---
layout: post
title: "Testing with Visual Studio and .NET 5 (2021)"
categories: Programming
excerpt: Automated tests is one of the most effective ways to be confident that your code actually works.
---

<iframe width="560" height="315" src="https://www.youtube.com/embed/BBz8DP10kIA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Automated tests are one of the most effective ways to be confident that, when developing software, your code actually works as expected.

Testing your code is instrumental to:

- Improve code quality
- Reduce bugs
- Increased confidence in your code
- Automate regression testing
- Refactoring your code.

## Why Should We Test?

The reason why we would want to test our code is to ensure that our code works, under varying circumstances, with different inputs. Depending on the program you write, your user may not enter inputs that you would normally expect, and so knowing how your code will behave when this happens, is good to know and whether that behaviour is expected or even acceptable.

Testing also improves the quality of your code, you'll find that when you have tests in place, the quality of your code will improve, this could be due to being certain, that the behaviour of your code is working correctly therefore giving you confidence to alter and improve it without breaking the underlying logic or functionality.

It also helps you focus on quality because you're having to think about all of the scenarios you need to test, it may even highlight that there are areas in your implementation which need to be addressed such as error handling or failing gracefully in order to keep the user experience of your application smooth.

An advantage of testing is that once the tests are written and passing, they are very repeatable. Meaning you can run them as frequently as you want and they should succeed every time, and if at any point during the development cycle some tests are failing, it's likely due to any updates or edits made to the codebase since.

## How to Test?

Basically it is you writing methods to test other methods in your code base. These are often written in a test project or within its own directory

You arrange the environment or scenario which will include preparing your code to be invoked by the test method and then asserting what outcome you are expecting

Each test ideally will cover a scenario within your code, this includes if/else statements, cases, loops.

Anywhere there's logic and has some functionality should have tests to cover those lines of code to minimize or remove any unexpected behaviour your code may encounter.

## Advantages


The benefits of doing all of this is that you can perform what's called a regression test. Meaning if you make updates to your code, running your tests again will inform you whether the functionality is still intact, despite any updates you've just made.

Bear in mind, that regression testing is not exclusive to automated tests, some companies have QA departments to do manual regression testing for their products, but understandably, automated tests ran by the codebase will not only be faster, but is repeatable, consistent and less prone to human error or oversight.

You can also automate the setup and tear down of each test to make sure the scenario and environment is the same every time.

Tests can also be treated as documentation for any developer who maintains the source code, some projects are large and it is unlikely that any one developer will remember every piece of logic that is written, so well written tests with good titles can be used to document business logic and other functionality.


## Disadvantages


It requires more time up-front. Not only does the developer have to write the functionality but the tests as well. Tests need to be  thorough and covering all the edge cases will take time.

The second disadvantage is that the tests are only as good as the developer who writes the tests, if the tests are poorly written or not thorough, then relying on those without any other regression test increases risk. If your tests are brittle, then they can also require time to "fix" those tests whenever you add logic even though the actual functionality hasn't actually been altered.

It's harder to test UI with these tests so having a QA team or the developer, manually check the UI is still required.

## Summary &#x1f4dd;

Testing is a common requirement for most job roles, being able to test your code well is a must-have skill for any junior developer wanting to get into the industry. It is often overlooked when learning, but spending some time to understand the concepts and getting good at testing is a worthwhile use of time.