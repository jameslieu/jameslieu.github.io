---
layout: post
title: "Writing Code Too Quickly"
categories: Programming
excerpt: Writing Code very quickly does not necessarily mean you're being more productive and can actually increase the amount of time to complete a task.
---

Writing Code very quickly does not necessarily mean you're being more productive and can actually increase the amount of time to complete a task.

When writing an email, it's not uncommon to not realise that there are errors or something missing (i.e. file attachments) in the email before you send it.

These problems are also present when coding. Not taking the time to plan and proof-read you code can lead to problems which are easily mitigated if you adopt a slower and more methodical approach.

## The Process &#x1f4dd;

I used to "try" to write code very fast. I would write code quickly but often not identifying the problem and solving it in a sensible way. I would find that I'm spending an large amount of time debugging but at the same time not really understanding the problem I'm trying to solve.

For example, when a unit test is failing, I discover where I think the problem is, start to tweak it, and run the test to see if it passes, if it fails I repeat that process again and again until it passed. It looked something like this:

**Step 1:** Make a change.

**Step 2:** Run test.

**Step 3:** If the test fails, repeat step 1.

Imagine doing this over and over until the test finally passes. During this process, because I'm 'rushing', there can be typos or missing characters in my changes, which I only discover because the tests notified me when it failed or if the complier fails the build.

If that didn't work, I would do a lot of [copy-and-pasting](/copy-and-paste-programming) either with blocks of logic or functions from the source code with slight changes. Or I look on the internet for solutions and copy the code from there.

Having a decent typing speed and using a few keyboard shortcuts on the IDE motivated me to churn out code as quickly as I can.

It sounds like a great at first glance but there were some serious flaws with this way of working. So I thought I might list my opinions on the pros and cons of this style of coding.

## Pros &#x1f44d;

### &#x1f4aa; You feel more productive

You'll find that you're very focused on the task, typing in so many lines of code, running your unit tests to get them to pass as you debug or tweak the logic to correct a bug or issue with the application.

As you're doing this, time is going by very quickly, you feel good at how focused and productive the day has been.

### &#x1f3c3; It's sometimes faster

The increased speed in which you're working can mean that you're getting things done faster, providing that the solution you've written works and there were no issues.

If enough time and effort is spent on the requirements and prerequisites prior to coding, then often this way of working is fine and feels great when you have a plan.

## Cons &#x1f44e;

I'll list the ones based on my own experience as well as some ideas how to address them.

### &#x1f926; You're more prone to mistakes

You're more likely to make these mistakes if you don't pace yourself; things like typos, using the wrong variable or misreading the code can really halt your productivity.

**Solution: Pace yourself, focus on one step at a time and be sure to read your code as you write it.**

### &#x1f644; You don't read the code

You'll find that 'skimming through' the code is faster and matches your pace of working. This is more obvious when self-reviewing your own code, rushing to push the code up as soon as possible can encourage you to 'skim through' your code and risk missing any flaws with the code.

Some of the issues you might introduce are typos, refactoring opportunities, commented-out code, unused code and duplication.

**Solution: Read your code often.**

### &#x1f62c; You haven't actually identified the problem you're trying to solve

The urge to start coding before coming up with a plan can hide what the real solution or problem is. The solution often isn't something that's obvious, you may have an idea how to write it, but what if that idea is incorrect?

This has happened to me numerous times. You'll spend hours on a task only to realise that your solution is flawed or even wrong.
You can be so focused on the task that you don't realise the time and have spent potentially hours on it before asking for help.

You speak to a co-worker to see if they can help you, and you both immediately realise that your solution needs to be updated or improved. Even worse if you end up realising this as you were explaining problem to begin with. See [Rubber duck debugging](https://en.wikipedia.org/wiki/Rubber_duck_debugging) &#x1f986;

**Solution: Take a moment to make sure you understand the problem, it helps to plan how you're going to tackle the problem by writing a checklist or some key points on what the problem is.**

### &#x1f64a; You Forget Something

Not only are you more likely to make mistakes when coding too quickly, you're more likely to miss something. When you've finally gotten that unit test to pass. You may feel that you're done, commit your code and push your changes without thinking whether you may need to do anything else.

A common example would be to run the full test suite again, new logic you have written may have broken another part of the system. So the tests will fail and you'll need to fix it. It is especially bad if the test suite takes a very long time to run.

Another key example is the organization of your work, particularly for version control. A good practice when working with Git for example is to commit regularly and to keep your commits. When working too quickly, you may forget to commit and if  you're working on a large feature. This can be problematic if you haven't completed the work and you needed to commit the code to hand-over to someone else.

**Solution: Commit and self-review your own code regularly**

### &#x1f41e; You spend more time debugging

Probably the main sign and negative aspect of coding too fast.

Your code doesn’t work and you find yourself chasing tons of bugs and issues.
You end up spending more time trying to fix problems rather than think about the problem and solution.

**Solution: Code a little bit at a time, test and verify it before moving on to the next step.**

### &#x1f649; You lose understanding of how your code works

When working this way, after a while of trying to fix the bug, you may find that you've made so many changes and tweaks to get the tests to pass, that you've changed too much and no longer know what you're code is doing.

And so you'll attempt to undo (**CTRL+Z**) everything in order to get it back to the state it was in before all of those changes you made.

**Solution: Take a step back and make sure you understand the problem and the solution.**

## Summary &#x1f4dd;

Often those who write the code the fastest in terms of time are those who are methodical and slow about the process. Attempting to rush the work can lead to many problems if you're not careful. Slowing down and being methodical in your way of working is not only a safer but also less stressful.

Developers aren’t measured on how fast they write code but by the quality of the solution and how well it works and maintainable it is. The best code is written slowly and purposefully, not quickly with the intent of meeting an arbitrary deadline.
