---
layout: post
title:  "Mocking In JS"
categories: Programming
excerpt: Proxyquire VS SinonJS
---

The purpose of this post is to compare the libraries we're currently using for mocking in our tests.
The two primary libraries we're using are `Proxyquire` and `Sinon`. 

At the moment we're using those interchangeably, and there seems to be some confusion to which one we should use or sometimes even both are used in the same test. The initial motivation for writing this blog was because of some of the challenges or confusion that we have faced when attempting to mock/stub the AWS SDK in our unit tests. So I have put together these notes to compare the ways we can achieve the same test for each library.

---
###### [Proxyquire](https://github.com/thlorenz/proxyquire)

- Takes over require and lets you inject fakes anywhere in the dependency chain.
- Thus it still loads the original, just replaces things with what you define.

###### [SinonJS](https://github.com/sinonjs/sinon)

- Doesn't take over require
- It's a more traditional mocking framework. 
- Replace specified methods with fakes, or create a mock that tracks when it was called.

---


##### Examples

Here is some example code I can use to demonstrate both Proxyquire and Sinon to see the difference.


Consider the following implementation:

```javascript
const aws = require('aws-sdk');

exports.exampleFunction = () => {
    const sqs = new aws.SQS();
    const receiveParams = {
        QueueUrl: 'http://example.com',
        MaxNumberOfMessages: 10,
        WaitTimeSeconds: 1
    };

    return sqs.receiveMessage(receiveParams).promise()
        .then(msg => sqs.sendMessage(msg).promise());
}
```

This is a basic example of using the aws-sdk library. We have an exampleFunction which calls SQS’s receiveMessage which then calls the sendMessage if the call was successful. If the sendMessage call is successful we assign the response to the result variable which is then returned.

Below we’ll show an example of how we might write a unit test (for success) for this with each library so we can compare the two:

###### [Proxyrequire](https://github.com/thlorenz/proxyquire) Example
```javascript
const proxyquire = require('proxyquire');
const test = require('ava');

test.serial('test exampleFunction returns bar', async t => {
    let AWS = {
        SQS: function () {
            return {
                receiveMessage: () => {
                    return { promise: () => { return Promise.resolve() } }
                },
                sendMessage: () => {
                    return {
                        promise: () => { return Promise.resolve('bar') }
                    }
                }
            };
        }
    };

    let awsSdkSqsExample = proxyquire('../src/aws-sdk-sqs-example', {
        'aws-sdk': AWS
    });

    var actual = await awsSdkSqsExample.exampleFunction();
    let expected = 'bar';

    t.is(actual, expected);
    t.pass();
});
```

With Proxyquire, we can take over the require statement to import the exampleFunction but also creating fake data to replace the actual aws-sdk functions in order to assert the values we want. Proxyquire will only replace the functions which we define while still allowing the other available functions to work and be used as normal. Which means Proxyquire can work very well as a feature test.

One thing I also noticed (particularly with this example) was that there interesting behavior in regards to validation. The receiveMessage function has validation. If the receiveParams passed in were to be invalid, then the Promise will be rejected. This can be considered a positive or negative outcome as it encourages the tests to be written with valid parameters but at the same time its not a true mock/stub and was a little unexpected.

One thing you can’t do is assert the stub. we can only assert the values based off what we’ve stubbed and returned

###### [Sinon](https://github.com/sinonjs/sinon) Example
```javascript
const awsSdkSqsExample = require('../src/aws-sdk-sqs-example');
const AWS = require('aws-sdk');
const sinon = require('sinon');
const test = require('ava');

test.afterEach(function () {
    sinon.restore();
});

test.serial('test exampleFunction returns bar', async t => {
    var sqsStub = sinon.stub(AWS, 'SQS');
    var receiveMessageSpy = sinon.spy(() => {
        return {
            promise: () => { return Promise.resolve() }
        };
    });
    var sendMessageSpy = sinon.spy(() => {
        return {
            promise: () => { return Promise.resolve('bar') }
        }
    });

    sqsStub.returns({
        receiveMessage: receiveMessageSpy,
        sendMessage: sendMessageSpy
    });

    let actual = await awsSdkSqsExample.exampleFunction();
    let expected = 'bar';

    sinon.assert.calledOnce(receiveMessageSpy);
    sinon.assert.calledOnce(sendMessageSpy);
    t.is(actual, expected);
    t.pass();
});
```

Sinon is considered a 'true' mock/stub/spy framework. It is also familiar in its use case.

The external libraries/classes/functions are completely mocked and thus allowing more flexibility, particularly with asserting them (including the number of times a mock as called). Not only can we determine what is returned from a function, we can configure the different return values depending on how many times a function is called i.e. a difference value if the function was called a second time.

###### Proxyquire with Sinon Example
```javascript
const proxyquire = require('proxyquire');
const sinon = require('sinon');
const test = require('ava');

test.afterEach(function () {
    sinon.restore();
});

test.serial('test exampleFunction using both proxyquire and sinon', async t => {
    let sqsStubs = {
        receiveMessage: sinon.stub().returns({ promise: () => Promise.resolve() }),
        sendMessage: sinon.stub().returns({ promise: () => Promise.resolve('bar') }),
    };

    let AWS = {
        config: {
            update: sinon.stub()
        },
        SQS: function () { return sqsStubs }
    };

    let awsSdkSqsExample = proxyquire('../src/aws-sdk-sqs-example', {
        'aws-sdk': AWS
    });

    var actual = await awsSdkSqsExample.exampleFunction();
    let expected = 'bar';

    t.is(actual, expected);
    sinon.assert.calledOnce(sqsStubs.receiveMessage);
    sinon.assert.calledOnce(sqsStubs.sendMessage);
    t.pass();
});
```

It is possible to use both at the same time. Although its worth considering what value this might bring if the test can be achieved with just one of them.

###### [aws-sdk-mock](https://github.com/dwyl/aws-sdk-mock) Example
```javascript
const awsSdkSqsExample = require('../src/aws-sdk-sqs-example');
const AWS = require('aws-sdk-mock');
const test = require('ava');

test.afterEach(function () {
    AWS.restore();
});

test.serial('test exampleFunction returns bar', async t => {
    const receieveMessageResponse = {
        QueueUrl: 'http://example.com/test',
        MessageBody: 'test 123',
    };

    AWS.mock('SQS', 'receiveMessage', function (params, callback) {
        callback(null, receieveMessageResponse);
    });

    AWS.mock('SQS', 'sendMessage', function (params, callback) {
        callback(null, 'bar');
    });

    let actual = await awsSdkSqsExample.exampleFunction();
    let expected = 'bar';

    t.is(actual, expected);
    t.pass();
});
```

Its worth also mentioning that specifically for mocking the aws-sdk there is another library we can use, aws-sdk-mock. This library is really designed for syntactic sugar and actually uses Sinon to do its mocking. It does look cleaner and more readable. So this can also be an option to consider as well. There does seem to be a limitation for asserting whether the mock was called but I believe there is an option to use a “Sinon Spy” with this library which then allows for adding those assertions.

#### Summary

Any of the above libraries are fit for our use cases. And there’s nothing particularly wrong with using all three. And the examples that were provided are very basic and may not even be the best way of writing those tests, there are more functionality and utility that I can see in the official documentation so its worth having a look at those as well (links are at the bottom).

Its worth thinking about considering some consistency in how we use these libraries, to avoid confusion as well as improve maintainability of our own tests.

For some, Proxyquire feels more intuitive than Sinon. Once the ‘stubs' are defined, its can become clearer to read what will happen once those are called. The advantage of defining exactly which functions needs stubbing allows for the some degree of 'feature testing’ which can be useful.

If we’re unit testing, we need to decide how ‘isolated' is our test going to be, if we’re intending to test in full isolation then Sinon would be a better fit. Not only does it fully mock/stub the external libraries/functions (including assertions), but we’re also familiar with its ‘style' as it is similar to other mocking frameworks we’re used to and currently using in other projects.

---

#### External Resources

[https://github.com/thlorenz/proxyquire](https://github.com/thlorenz/proxyquire)

[https://github.com/sinonjs/sinon](https://github.com/sinonjs/sinon)

[https://github.com/dwyl/aws-sdk-mock](https://github.com/dwyl/aws-sdk-mock)
