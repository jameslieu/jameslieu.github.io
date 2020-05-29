---
layout: post
title: "Copy-and-paste Programming"
categories: Programming
excerpt: What is copy and paste programming?
---

## What is copy and paste programming?

According to [Wikipedia](https://en.wikipedia.org/wiki/Copy-and-paste_programming):

 > Copy-and-paste programming is the production of highly repetitive computer programming code, as produced by copy and paste operations.

I've begun experiencing this at work lately, We have a microservice architecture and each of these services are ASP.NET Core applications which are very similar to one another. When we need to create a new service, the infrastructure, packages/libraries and design of these services have similar requirements and can be ported across very easily by copy-and-pasting.

###### What is the issue?
The issue I have is, that we've learned and improved since the creation of some of these older services but when copying the code across to the new service we tend to copy over **everything**. And this **process** of copying everything sometimes doesn't include reading the code or file and considering whether it is relevant to port across.

Often the ticket to create this new service only requires us to create a new project that mimics the older services `/ping` endpoint and a unit test. Also to port across some of the core infrastructure code such as the logging configuration, and any dependencies such as libraries as well. It makes sense to copy-and-paste those across, but should things like helper classes, unused libraries, test helpers and unused common classes be copied across as well?

There is an argument for copying those across if we know we're going to use them eventually. The issue with this is that it adds risk to include code we may not use at all. My suggestion to avoid this, is to only copy across code as and when you need them.

There was a good [StackOverflow post](https://stackoverflow.com/a/15700228/2405120)  about removing unused code which I think is relevant.


Below I'll run through my opinion on what the pros and cons are for copy-and-paste programming.


## Pros &#x1f44d;

###### &#x1f3c3; Its faster
It is in fact faster to do it this way. We know that the infrastructure is going to be mostly the same, why not just copy and paste the lot across and rename places that need it i.e. Namespaces. And by completing the task faster, we can move on to the next task thus feeling very productive

###### &#x1f60f; No need to think as much

When copy and pasting the code across, if you intend to reuse everything, you can do it without too much mental energy.

## Cons &#x1f44e;

###### &#x1f9d0; It creates new challenges when reviewing the code

The more code we port across, the easier it is to miss something. The initial ticket was to create a base/plain project which should ideally have only the necessary modules needed, now that there is other code in there, the reviewer now has to go into the code base and check which is being used and which isn't.

Having to check each class or method and see if it is needed or not is incredibly time consuming.

It also causes confusion why those unnecessary classes are there at first glance. And asking the developer to remove the dead code requires even more time.

###### &#x1f4ca; It invalidates the code coverage

The Code that isn't used in the new project messes with the code coverage, while in the previous projects they were used and had unit tests. The new project wouldn't have those same tests as the methods using them are not ported across.

There is an argument that maybe some of those classes ought to have their own self contained unit tests however.

###### &#x1f9f9; It takes away the 'refactoring' opportunity

Technically its not refactoring because its a new project, we're not editing existing code in the new project. But over time, we as a team are improving the way we work and our knowledge, sometimes the code we're copying across is perhaps an 'outdated' way of working. This can deter the developer to consider a different approach.

######  &#x1f648; The developer may not even read the code

Entire files can be copied across, how will we know whether the code is still relevant to the new project. Not only this, it is the review who has to read it all during the code review. That said, the reviewer may also have the same mindset and approve the code because they know that it is a carbon copy-and-paste and therefore doesn't feel the need to read it.

######  &#x1f649; There is risk that the developer doesn't understand the code

Code that is copied across may have been code that they themselves haven't seen before, instead of reading it and trying to understand the business logic, copying it across can mean you're adding code that may not be relevant or even is an existing bug.

###### &#x1f41e; Introducing bugs
A further problem is that bugs can easily be introduced by assumptions and design choices made in the separate sources that no longer apply when placed in the new environment.

###### &#x1f9d0; Obfuscated code
Such code may also, in effect, be unintentionally obfuscated, as the names of variables, classes, functions and the like are typically left unchanged, even though their purpose may be completely different in the new context.

---

## Summary &#x1f4dd;

Copy-and-paste programming sounds good at first. Its a very attractive way of working as it can make you feel very productive, it also means you can quickly move on to other tasks/tickets.

But the number of problems that it can introduce is something to consider. I'm not advocating that we never use copy-and-paste but I think its worth actually reading the code and carefully consider whether that code is relevant. But to also take a moment to think whether that code can be improved. Sure it will take a little longer, but also reduce some of the cons above makes it worthwhile.



### External sources &#x1f4a1;

[Wikipedia - Copy-and-paste Programming](https://en.wikipedia.org/wiki/Copy-and-paste_programming)