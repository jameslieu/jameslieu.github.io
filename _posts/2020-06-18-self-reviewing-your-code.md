---
layout: post
title: "Self-reviewing Your Code"
categories: Programming
excerpt: Self-reviewing your code is, in my opinion, just as important as having someone else review it before it gets approved and deployed.
---

Self-reviewing your code is, in my opinion, just as important as having someone else review it before it gets approved and deployed. It is akin to proof-reading an email you wrote before sending it; checking that you haven't missed anything, whether there are errors or whether there are areas you can refine.

Not self-reviewing adequately is probably more common than we think, I myself have been guilty of doing this. When you think you're done coding your feature, it is easy to skim through your changes (diff) or not look at them at all. Submit the change. Then let your colleague review it while you work on a new and more exciting task.


## Why Should We Self-Review Our Work? &#x1f914;

It is conceptually the same reason we proof-read any emails or any writing intended for someone else. You'll want to catch errors, look for areas which can be refined and check if anything was missed or had been forgotten.

Often re-reading your code again can give you further confidence that what you've worked on is done to a standard that you deem acceptable when contributing to the product you're working on. Also, depending on the size of the work, when working on a particular feature long enough can reduce the likelihood that we'll to remember **exactly** what was added and what was removed.

## What's the worse that could happen? &#x1f937;

From the perspective as a developer for a company, it depends on the scenario really, if you're working on a system that is only used within the company internally then it's not as detrimental if you deploy work that breaks the system.

Another example is a product that doesn't have any 'live' users. There is more leeway for errors or issues under these circumstances. Although, it will not only cause inconvenience for you but for your team members as well.

It is, however, very serious if the system is used by clients or customers and is a source of revenue for your company. In under any circumstances should anyone be deploying work without being absolutely certain that the changes do not break the system unknowingly. It's bad for the customer, its bad for the team and it's bad for the company. Everybody is unhappy, so being extra careful when making changes or updates to the system is paramount.

## Reviewed by somebody else &#x1f575;

It's a standard practice to have your code reviewed by someone else before it gets released to production. We're all human and are not infallible, having a second pair of eyes on your code to check for errors, look for improvements and to make sure that it meets the requirements is very valuable and should not be taken for granted when working in a team.

The code review process has some acceptable trade-offs. The first is that it requires a member of your team to 'review' said code, which means that time needs to be allocated to that task. The reviewer will need to read the code and if there is feedback or changes requested, then the code owner needs to either go back to modify the code or to have a discussion about it.

This takes up a fair amount of time and even more so, if there were obvious defects in the code which would've been spotted had the developer been more vigilant with reviewing their own work.

Having the reviewer leave feedback for 'commented-out' code or typos are not only embarrassing but requires time allocated to fix it. Vigilantly self-reviewing your code can at least mitigate those kinds of errors.

It's arguably selfish to leave the fault-finding to the reviewer, as mentioned previously, this review process can take time. How can we expect someone else reviewing your work and to be vigilant if we don't abide by the same standard. At the very least, the developer ought to respect their own work by self-reviewing and making sure that what they're submitting is done to a high standard.

Relying on the reviewer to find those because they feel that reviewing their own code will 'slow' them down is not only egotistical but a disservice to themselves as the more mistakes they submit, the less confidence the rest of the team will be in the quality and skills of said developer.

### &#x1f9d4; My Personal Experience

I once had a colleague who did exactly this. He likes to work quickly which [has it's own problems](/working-too-quickly), he would open a pull request and then move onto the next task. When I began the code review, it was very often littered with issues, commented out code, code that was used for debugging purposes i.e. `console.log("here!!!!")` etc.

After the review, it needs to go back into progress, but my colleague would often be in the middle of the next task, which meant that he wouldn't pick up the work that was reviewed until the next day or even a few days after depending on how long it would take him to complete the task he was currently working on (which then a PR is created for it for review).

Because there was little self-review even for working on the feedback on the first PR, when that one goes back into review, it is not uncommon for that one to also have issues or require changes again. So the cycle continues

The problem was that reviewing like this takes a lot of time. Although the code owner felt he was being very productive, but in terms of the productivity from the team as a whole, we were at risk of not completing all the work we had allocated for that sprint. Productivity is compromise and all he had to do is read his own code to reduce the odds of the work to require updates or changes, especially for the obvious defects such as commented out code.

Bear in mind that I also have tasks of my own that I need to complete (and have reviewed).

## Summary &#x1f4dd;

To summarize the key points why self-review is important and worth the time:

- Check we haven't missed anything
- Check whether there are errors
- Check for areas for refinement
- Can identify areas of improvement
- A better team code review experience

I think habit of self-reviewing your code is one of the things that will improve the quality of the code you write. We're not infallible and should almost expect to write code that is imperfect. Self-reviewing simply allows us to allocate time to **think** about what was written, check for issues or anything you've forgotten or to look for ways to improve it.
