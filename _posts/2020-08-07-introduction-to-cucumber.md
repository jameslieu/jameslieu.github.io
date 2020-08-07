---
layout: post
title: "Introduction To Cucumber"
categories: Programming
excerpt: What are cucumber tests and why might they be useful
---

<img src='/assets/media/cucumber-tests-1.png' style="height: 50px; margin:0 auto" />

## What is Cucumber? &#x1f952;

[Cucumber](https://cucumber.io/) is an open source tool for running automated tests written in plain language.

Because they're written in plain language, they can be read by anyone involved with the product development. And it can be used to help improve communication, collaboration and trust.

<img src='/assets/media/cucumber-tests-2.png' style="height: 200px" />

Cucumber reads executable specifications written in plain text, it validates the software’s behaviour based on those specifications and they consist of multiple scenarios and each scenario has a list of steps for Cucumber to work through.

It verifies that the software conforms with the specification and generates a report, indicating success or failure for each scenario.

In order for Cucumber to understand the scenarios, they must follow some basic syntax rules, called Gherkin.

## Gherkin Syntax &#x1f4ac;

So Gherkin is the language Cucumber uses to define test cases. It’s a set of grammar rules that makes plain text structured enough for Cucumber to understand.

<img src='/assets/media/cucumber-tests-6.png' />
_Example of Gherkin Syntax_

It's designed to be non-technical, human readable, and collectively describes use-cases relating to a software system and seeks to enforce firm, unambiguous requirements. As well as document how the system behaves.

<img src='/assets/media/cucumber-tests-5.png' />
_Gherkin also supports over 70 languages, this is written in Portuguese_

### Keywords &#x1f50d;

Gherkin uses a set of special keywords to give structure and meaning to executable specifications. Most lines in a Gherkin document start with one of those keywords.

##### &#x26f2; Feature
The purpose of the Feature keyword is to provide a high-level description of a software feature, and to group related scenarios. The first primary keyword in a Gherkin document must always be Feature.

##### &#x274e; Scenario or Example.
This is a concrete example that illustrates a business rule which consists of a list of steps.

You can have as many steps as you like, but it’s recommended not to have too many. Having too many steps in an scenario, will cause it to lose it’s expressive power as specification and documentation.

### Steps &#x1f463;

The **Given** steps are used to describe the initial context of the system. It’s typically something that’s happened in the past.

When Cucumber executes a **Given** step, it will configure the system to be in a well-defined state, such as creating and configuring objects or adding data to a test database.

The **When** steps are used to describe an event, or an action. This can be a person interacting with the system, or it can be an event triggered by another system.

The **Then** steps are used to describe an expected outcome, or result. It should use an assertion to compare what the system actually does, to, what the "Step" says the system is supposed to do.

<img src='/assets/media/cucumber-tests-3.png' style="height:320px;" />
_Example "Steps" of an API call to search for a contact_

If you have successive **Given's**, **When's** or **Then’s**, you can use **And** or **But**.

### Step Definitions &#x1f4ad;

Cucumber tests are divided into individual Features. These Features are subdivided into Scenarios, which are sequences of Steps.

Steps can be considered a method invocation. Before Cucumber can execute one, it must be told how that step should be performed via a Step Definition.

Step definitions are the glue between, features written in Gherkin, and the actual test’s implementation.
They connect Steps to programming code and carries out the action that should be performed.

<img src='/assets/media/cucumber-tests-4.png' />
_Step Definitions for the above "Steps" example_

They are methods with an expression, that links it to one or more Steps.

So when Cucumber executes a Step in a scenario, it will look for a matching Step Definition to execute.

## Key Points &#x1f511;

So just to run through some of the key points

- Cucumber is an Open source tool for test automation
- It reads executable specifications written in plain text.
- The test-cases are written in a language called Gherkin.
- Step definitions connect Gherkin steps to programming code via an expression

## Summary &#x1f4dd;

So the question remains. Why?

Why might we want to write cucumber tests? Bearing in mind that this could be **in addition to unit testing**. What might we want to achieve? What is the goal of testing?

### "To increase confidence for stakeholders through evidence - Dan North"

This is a quote from Dan North - the creator of behaviour driven development. What he means by “stakeholders” is people whose "lives" you touch i.e. your users. But it also can mean product owners, compliance, security, testers, support, other developers.

Cucumber tests are a form of testing, but you wouldn't just use Cucumber for that, you're using it to help communicate requirements. To not only increase confidence for stakeholders but also for yourselves.

---

#### External Resources

[https://cucumber.io/](https://cucumber.io/)

[https://github.com/cucumber/cucumber-js](https://github.com/cucumber/cucumber-js)

[https://en.wikipedia.org/wiki/Cucumber_(software)](https://en.wikipedia.org/wiki/Cucumber_(software))