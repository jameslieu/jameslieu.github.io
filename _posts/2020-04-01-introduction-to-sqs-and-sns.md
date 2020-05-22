---
layout: post
title:  "Introduction to SNS and SQS"
date:   2020-04-01 16:00
categories: aws
comments: true
---

So for this post I'll be covering a basic overview of Amazon's Simple Queue Service (known as SQS) and Amazon's Simple Notification Service (known as SNS).

<!--more-->

---

### Agenda

- What is SQS?
- What is SNS?
- The difference between SNS and SQS
- Advantages of using SNS and SQS together

I’ll be running through briefly, what is SQS before moving on to, what is SNS? The differences between the two and the advantages of using them together.

---

### What is Amazon's Simple Queue Service (SQS)?
<img src="/assets/media/sqs-logo.png" style="float: right; height: 200px;"/>

SQS is a fully managed message queuing service that enables you to decouple and scale microservices, distributed systems, and serverless applications.

Using SQS, you can send, store, and receive messages between software components at any volume, without losing messages or requiring other services to be available
&nbsp;
&nbsp;
&nbsp;

---

###### SQS offers two types of message queues:


| Standard Queues | FIFO (First in, First Out) Queues |
| --------------- | --------------------------------- |
| Unlimited Throughput: Support a nearly unlimited number of transactions per second per API action.  |  High Throughput: By default, FIFO queues support up to 300 messages per second |
| Best-Effort Ordering: Occasionally, messages might be delivered in an order different from which they were sent.  |    Exactly-Once Processing: A message is delivered once and remains available until a consumer processes and deletes it. Duplicates aren't introduced into the queue. |
| At-Least-Once Delivery: A delivered at least once, but occasionally more than one copy of a message is delivered.  | First-In-First-Out Delivery: The order in which messages are sent and received is strictly preserved (i.e. First-In-First-Out). |
| <img src="/assets/media/sqs-1.png" /> | <img src="/assets/media/sqs-2.png" /> |


#### Working with SQS Messages

- Messages are persisted and is stored for some configurable duration. The default is 4 days but it can be up to 14 days before they’re automatically deleted.

- Messages can contain up to 256 KB of text data, including XML, JSON and unformatted text
- An external service is needed to poll and grab messages from SQS to process. Once the service has successfully processed them, the message can be deleted from the queue.

- Alternatively, you can configure your queue to trigger a lambda function to process the message. The lambda will only delete the message from the queue if your function has returned successfully without any errors. If the function fails to process, a **dead-letter queue** can be leveraged to store those failed messages

#### What is a Dead-letter queue (DLQ)?

A dead-letter queue is simply an SQS queue for messages that can't be delivered successfully, for example due to client or server errors.

Those messages can be held in this queue for reprocessing, we can also configure an alarm for messages arriving into this queue, as well as examine them for further analysis

### Quick Summary

- A fully managed message queuing service
- Send, store, and receive messages
- Supports Lambda triggers
- Dead letter queue support

So just a quick summary, SQS is a fully managed queuing service. It can send store and receive messages. It supports lambda triggers and can be used as a dead letter queue for storing failed messages.


---

### What is Amazon's Simple Notification Service (SNS)?
<img src="/assets/media/sns-logo.png" style="float: right; height: 200px;"/>
SNS is a fully managed publish/subscribe messaging service that coordinates and manages the delivery or sending of messages to subscribing endpoints or clients.

It provides ‘topics’ which are messaging channels that any number of subscribers can subscribe to. When the Topic receives an event or message, it pushes it to all subscribers at the same time.

&nbsp;
&nbsp;
&nbsp;


There are two types of clients to be aware of, subscribers and publishers

<img src="/assets/media/sns.png" />

#### Subscribers

- Web servers
- Email
- SQS queues
- Lambda functions


Subscribers (i.e. web servers, email addresses,  SQS queues,  Lambda functions) consume or receive messages from the topic they’re subscribed to.

#### Publishers

Publishers such as distributed systems, microservices and other AWS services can communicate asynchronously with subscribers by producing and sending messages to an SNS topic


### Basic Usage

<img src="/assets/media/sns-2.png" style="height: 250px;" />

To use SNS, a topic needs to be created. We can control access to it by defining policies that determine which publishers and subscribers can communicate with it.
 
A message is sent directly to the topic. SNS matches the topic to a list of subscribers who have subscribed to it, and delivers the message to each of those subscribers.

I’ll run through some common scenarios.

#### Scenario 1: Message Fanout

So message fanout occurs when a message, is published to a topic, which is then pushed to multiple subscribers or endpoints.
This provides asynchronous event notifications, which in turn allows for parallel processing.  
 
<img src="/assets/media/sns-3.png" style="height: 250px;"/>

For example, imagine a topic which has some SQS queues subscribed to it, and imagine we have an application that sends a message to this topic whenever an order is placed for a product.

When an order is placed, the SQS queues would receive identical messages for that new order at the same time. A service receiving the message from one of the queues could be responsible for the processing of the order, while the other queue can be used by a different service to store the ‘order data’ in a database.

<img src="/assets/media/sns-4.png" style="height: 200px;"/>

#### Scenario 2: Application and System Alerts

Application and System alerts, so notifications or alerts that are triggered by a breach of predefined thresholds for monitoring for example

<img src="/assets/media/sns-5.png" style="height: 150px;" />

#### Other Scenarios

Other Scenarios can be:

- Push email or text messaging i.e. Targeted news headlines to subscribers by email or SMS
- Mobile push notifications i.e. Send messages directly to mobile apps, indicating that an update is available for example.

<img src="/assets/media/sns-6.png" style="height: 250px;" />


### Message Delivery Retries

SNS defines a delivery policy for each delivery protocol. The delivery policy defines how SNS, retries the delivery of a message if it is undeliverable for whatever reason.
 
Apart from HTTP, delivery protocols do not support custom delivery policies, so you can’t customise SNS-defined delivery policies.

When the delivery policy is exhausted, SNS stops retrying the delivery and discards the message. Although, if a dead-letter queue, is configured to the subscription however, then the message will be held there. The dead letter queue is configured on the subscription rather than a topic because message deliveries happen at the subscription level.

<img src="/assets/media/sns-7.png" />

---

### The differences between SNS and SQS

| <img src="/assets/media/sns-logo.png" style="height: 150px;"/>  | <img src="/assets/media/sqs-logo.png" style="height: 150px;"/>  |
| --- | --- |
| Fully managed publish-subscribe system.  | Fully managed Queuing system |
| There is no persistence. So the message isn’t stored by SNS.  | Decoupling applications / Parallel asynchronous processing |
| Fanout - Processing the same message in multiple ways | Messages are persisted for some (configurable) duration |
| Push mechanism - Messages are pushed to subscribers/consumers | Pull mechanism - Receivers must poll and pull messages|

SNS is a distributed publish-subscribe system.  There is no persistence, so the message isn’t stored by SNS.
Leveraging SNS allows for processing the same message in multiple ways and at the same time. It uses a push mechanism, so messages are pushed to subscribers.

Whereas SQS is a queuing system, used for decoupling applications and allowing parallel asynchronous processing.  Messages are persisted and is stored for some configurable duration. It can be up to 14 days before they’re automatically deleted
SQS uses a pull mechanism – So messages are NOT pushed to receivers. Receivers would have to poll or pull messages. Although SQS does support lambda triggers so we don’t necessarily have to poll for messages, we can leverage that instead.


### Why might we use SNS with SQS together?

<img src="/assets/media/sns-8.png" style="height: 250px;" />

There may be different kinds of subscribers of the same topic where, some need the immediate delivery of messages such as alerts or email. But others might require the message to persist, for later usage or processing.

##### Asynchronous Processing
When a message is published to a topic, it can be distributed to multiple SQS queues which can then be processed in parallel.

##### Persistent Storage
By leveraging SQS, the message can be stored, the service can poll and receive the message as and when it decides. If the service were to become unavailable for some reason, the message would still be available within the queue.  Once the service is available again, it can then continue to poll and process those messages.

##### Dead letter queue
If SNS pushes a notification directly to a subscribed Service, and that service is unavailable, then the message will be lost. Leveraging dead-letter queues will solve this issue.

Also, even if the service has 'received' the message. What happens if an error occurs during processing or that processing fails? The message can be pushed to this queue making it available for repossessing or further analysis. And configured to only delete the message when processed successfully.

##### Achieve Guaranteed Delivery
So by coupling SNS with SQS, we can achieve guaranteed delivery by receiving messages at our own pace.

---

### Summary

So to summarize:
SNS distributes several copies of the same message to several subscribers, to be processed in parallel.
SQS is mainly used to decouple or integrate applications. It also allows clients to be offline and is tolerant to network and host failures.

Coupling the two together we can achieve:
- Parallel asynchronous processing
- Fault tolerant systems
- Guaranteed delivery

As well as the other benefits mentioned.

So that concludes my basic overview of the SNS and SQS.
We’ve covered what is SQS, what is SNS, the difference between the two and the advantages of using them together.
