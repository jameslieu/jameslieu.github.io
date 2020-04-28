---
layout: post
title: "Git Workflow"
date: 2020-04-28 12:50
categories: Git
comments: true
---

At a previous company, many of my colleagues had little to no experience with version-control. Git was recently introduced into their workflow :)

<!--more-->

### Background

I had just started a new role there, they were not using any version control (which led to many problems) and so Git was introduced into their workflow by the tech lead who had also just started his role a month prior.
Within the team and the work they were doing - there were so many issues:

- Huge merge conflicts
- Trying to commit without staging work
- Long-lived branches
- Out-of-date local master and feature branches
- Merging other people's branches
- Hot fixes for bugs
- Undoing commits or deleting them thus losing work
- etc

While I had just joined the team, I had worked with Git for a few years, so I was asked on many occasions to explain to my colleagues where they may have gone wrong and what they need to do to fix it. There was one QA engineer in particular who was struggling to grasp the basics even after many conversations with him. So I took it upon myself to prepare a document so the team can refer to if they get stuck or I can use to help explain things.

Here is the original document I wrote:

---

### Git Clarification

The first clarification I think is important to remember is the fundamental idea that Git tracks **Commits**.

Think of Commits as the **state** of the codebase. So, if you branch off master for example, you have all of master’s **Commits**. In the new branch you add some code then **Commit** it, your branch has those **Commits** including master's **Commits** (since you last git pulled) but master will not have your new **Commits** (until you merge them)

<img src="/assets/media/git-1.png" style="height: 500px;"/>

### Basic Diagram

This here is a basic diagram for what maybe is a typical feature you guys might be working on. The lines represent branches and the **Commits** are the represented by circles.

<img src="/assets/media/git-2.png" style="width: 600px;"/>

This example is the scenario of working on a feature with two user stories (**US-1** and **US-2**).
Master is branched off into a new ‘feature’ branch, then the feature branch is to be branched off into the **US-1** branch. **US-2** is also branched off the feature branch.

**US-1** is finished first, a pull request is opened then merged back into the feature branch (if approved). Meanwhile, **US-2** is being worked on, once it is ready, before opening a pull request, pull from the feature branch (which contains **Commits** from **US-1**), then open a pull request into the feature branch. This will allow your branch (**US-2**) to be ‘up to date’ with the feature branch if this makes sense.

Once **US-2** is approved and merged into the feature branch. A new pull request can be made from ‘feature branch’ to ‘Master’. This feature branch by now will contain **Commits** from both **US-1** and **US-2**

When everything is merged into master, we create a separate branch for the release. Remember, git only tracks the **Commits**, so in this scenario, the release branch will contain exactly the same **Commits** as master.

### Advance Diagram

The above diagram is designed to be basic so it’s easier to explain. The below diagram is designed to demonstrate exactly what is happening in the same scenario.

<img src="/assets/media/git-3.png"/>

One thing you have to bear in mind is that you have your Local Repository and there is a Remote Repository. Your local one is the one stored on your machine and the remote is on Azure DevOps.

Each repository will have their own branches. So technically (in this example) there are two master branches, one local and one remote. It is your responsibility to make sure that your local master branch is up to date with the remote master branch as it is possible that it has been updated since you’ve last ‘pulled’ down the changes into your local master while working on your feature.

When you're ready to open your pull request, you actually need to push your branch into the Remote repo

This example also demonstrates what happens if your pull request is rejected or requires some change. You add more **Commits** to your Local repo and then push those **Commits** to the Remote repo branch, it will just appear in the pull request to be reviewed again, you don’t need to create a new one.

After everything is approved and merged. A new release branch is created and you can pull master to update your Local master branch.

Note: These examples are under the assumption that a single developer is working on this feature. If there is a feature where the user stories are being worked on by multiple developers, then the feature branch would normally be available on the Remote Repo first, and you all work off that branch.

### Bonus: Hot Fixes

Here is an example how to deal with Hotfixes

<img src="/assets/media/git-4.png"/>

- Branch off the Release
- Fix/patch the bug.
- Open a pull request against the Release branch
- Merge if approved
- Merge into master as well

---

### My Thoughts

The above example demonstrates the Git workflow we were working with. I believe its commonly known as the [Gitflow Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow). We had release and feature branches along with tickets that had sub-tasks and/or user-stories which meant having to create a feature branch and branching off that to create 'user-story' branches. Not to mention applying patch/hot fixes. It isn't my prefered Git Workflow and anecdotally can be very confusing for beginners.

This kind of workflow requires a good understanding of how Git works and so it is unsurprising that the team struggled to grasp the basics and ran into so many issues. While I was happy to help them with this, it did take a lot of patience to explain and assist with their branches and commits, which at times were pretty disruptive for me.

I'm not necessarily saying that my document here is particularly good, and my diagrams/notes can be improved but I remember that I didn't want to spend too much effort on it at the time. Having look at those now, I wonder if they added to the confusion? I wouldn't know how else to simplify it further to be honest, it was a real challenge trying to teach my colleagues this topic, I could sense their frustration and sometimes their unwillingness to learn this topic at all. Having to explain to them 'why' was very difficult and I suppose they wished they could've reverted back to the old way of working before the tech lead had made this change.

### Conclusion

Thinking back on this experience, in my opinion, it was probably not a good idea for the tech lead to transition everyone to a new (version-control) system they were not familiar with, without first giving them time to learn and adapt.

It would've been much more effective to run through a workshop to teach the basics instead of carrying on and trying to fix the conflicts and challenges as they arise (to improve knowledge on Git). Also just sending an article/blog about Git via email is good but will not be effective if no one actually spends time to read it.

In any case, I would've prefered we used a more simple Git Workflow such as the [GitHub Flow](https://guides.github.com/introduction/flow/) to avoid overwhelming them with some of Git's more complicated features (present in the [Gitflow Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)) while they learn.

Maybe I'll one day, now that I have some experience with both Git Workflows, write a blog post to compare [Gitflow Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) vs [GitHub Flow](https://guides.github.com/introduction/flow/) and see the pros/cons of each workflow.
