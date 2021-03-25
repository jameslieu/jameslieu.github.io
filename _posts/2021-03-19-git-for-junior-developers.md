---
layout: post
title: "Git For Junior Developers"
categories: Programming
excerpt: How can we simplify learning Git?
---

<img src="/assets/media/git-logo.jpg" style="height:100px; margin: auto">

When learning Git, it had taken a while to actually understand it.

Having worked as a developer for a number of years I've found that I only really use a handful of git commands and so any learning for less commonly used commands like `Cherry picking` or `Rebase` was really unnecessary as a junior.

Those commands had a larger learning curve and often led to confusion and frustration when trying to use them.

I've also experienced working in a team who have never worked with Git and the tech lead wanted to move the whole team to Git without actually teaching them, this led to numerous problems as well as my own challenges trying to teach some of them. I've written a blog post about it [here](/git-workflow)

So the purpose of this post is to recommend **specifically** which commands are most commonly used (anecdotally), and what juniors need to know *at minimum* to get by in the industry.

## All you need to know &#x1f44c;

#### Prerequisites

- Know how to use the command line interface.
    - I recommend NOT using a Git GUI until you understand the basics
- Install Git to your local machine

## Basic workflow

<img src="/assets/media/git-workflow-5.jpg"/>

Here is a flowchart of what your basic workflow will look like, I've highlighted the commands you use to achieve each step. This is a fairly simplified chart but essentially this will be how you work with Git majority of the time.

There are going to be some steps inbetween depending on edge cases such as stashing code or reverting code using Git if you needed to, but otherwise this chart is pretty much Git in a nutshell.

#### Introduction

Git is software for tracking changes in any set of files, usually used for coordinating work among programmers collaboratively developing source code during software development.

In other version control systems, each developer gets a working copy that points back to a single central repository.

Git, however, is a distributed version control system. Instead of a working copy, each developer gets their own local repository, complete with a fully-tracked history.

This means that it is easy for developers to collaborate and even prevents any one developer from blocking the work from another because they would each have their own local repository.



#### Master
The `master` branch is the convention name for the "main" branch which is considered the code used for production. This branch is the base which you build upon, and so you would "branch" off this one to achieve to add new features or changes.

#### Branch
Think of **branching** as cloning or duplicating the code base, any edits you make to a new **branch** will not affect the original. When you're edits are complete you can then **commit** those edits and then **merge** your edits with the original (where you branched off from).

#### Commit
Ok to start, the first clarification to mention, is that Git tracks code with commits.

Think of Commits as the **versions** of the codebase, and each commit is it’s own version. When a developer is working on a Git repository, they’re usually working with the last or latest commit as that is the most up-to-date version of the codebase.

In fact, a developer can theoretically choose any existing commit on a Git repository they wanted to work on. So if it helps, Git commits are basically unique versions of the code base. Hence version control.

#### Feature Branches
Git utilizes a feature called branching. Although the word branch is synonymous with a branch of a tree or subdivision of a bank for example, in Git, it is actually easier, in my opinion to think of feature branches as a clone of the code base.

For example, if you have a project which uses Git, that project will have a branch by default. Git allows you to create a new branch on that project which essentially has the same state of the code base as the original branch you’ve branched off of.

Any edits you make to this new branch will not affect the original. When you’re edits are complete you can then commit those edits which at that time is only available to the branch you’re on. And you then have the option to merge your commits with the original branch.

<img src="/assets/media/git-workflow-1.png" style="height: 500px;"/>

The ability to branch off another branch grants numerous ways to collaborate or contribute to a project.

## Local Respository vs Remote Repository &#x1f680;
A project where Git is used is known as a **repository**.

**Local** repository means the project on your local machine or computer and is only available to you.

**Remote** repository is the project which is hosted by a Git based hosting provider i.e. [GitHub](https://github.com), [GitLab](https://gitlab.com) or [BitBucket](https://bitbucket.com)

The remote repository is what allows teams to collaborate against the same code base, making changes to code will almost always be done an a computer, so we need a "local" copy of the code base to do this, when you've made your branch, edits and commits.

You can then **push** branches including `master` to the remote making it available to your team via the internet. Your team can then have the option of **pulling** that code back onto *their* local machine and thus be able to access and make edits of their own.

<img src="/assets/media/git-workflow-3.png"/>

The key thing to bear in mind is that you need to actively try to keep both your local and remote repository as up to date as possible.
This also includes your local branches where you initially branched off master, but maybe later, the master branch has been updated since. So to deal with this, you can update your "local" master then `merge` your updated local master with your local branch.

So pushing and pulling regularly is a good habit to have.

## Advantages

Some of the other advantages relevant to developers are:

#### Being able to see what’s changed.
So Git tracks changes allowing you to see what has been changed since the last version. You can use that to quickly identify if any lines can be improved or even missing.

#### Quickly revert any changes you may not want,
Some developers may have used comments or logging code for debugging. Being able to see those lines and easily revert them is very useful.

Or even better, you may wanted to make a proof of concept or refactor some code but decide against committing that code, you can easily reverse all untracked or unstaged changes back to it’s last commit.

#### The source code is easily accessible
You can push your source code to a Git hosting service like Github, and anyone who has access can easily download the code to their local machine.

## My Most Used Git Commands &#x1f44d;

So I've looked at my `~/.bash_history` file, it records the last 2000 commands, so as of `18/03/2021` my most common `git` commands are:

| Command      | Count | Notes                                                                                   |
| ------------ | ----- | --------------------------------------------------------------------------------------- |
| git status   | 400   | I spam this to check for unstaged/staged code, and to look at branch name               |
| git checkout | 173   | Multiple uses, create branches, change branches, reverse changes                        |
| git pull     | 115   | Update en existing branch, commonly used to update `master`                             |
| git push     | 81    | Always with `origin <branch>`                                                           |
| git commit   | 40    | I use this with `-m` or to `--amend` them                                               |
| git add      | 37    | Sometimes I use a git editor to stage code, but I'm surprised this isn't higher         |
| git diff     | 34    | I only use this to check files changes before reversing changes with checkout           |
| git branch   | 35    | I only use this to delete my local branches with `-D`                                   |
| git log      | 20    | Only used to check logged commits either for myself or to see timestamp of latest       |
| git stash    | 17    | Stashing code and `pop`, for when needed to switch branches without commit              |
| git fetch    | 13    | Sometimes, new branches on remote need to be fetched                                    |
| git merge    | 10    | This is really used to update existing branches, I merge code to master via BitBucket   |
| git reset    | 3     | Used to undo a commit but I tend to use VSCode's built in GUI as it's easier            |
| git rebase   | 2     | Only if my local master needed updating alongside my local branch I was working with    |
| git init     | 2     | Initialize git for a directory, not commonly used when compared with others             |
| git clone    | 2     | Used to clone code in remote repository, not commonly used and usually copy/paste       |
| git config   | 2     | Use to set config, primarily changing the `autocrlf` to false, when running into issues |

It's worth noting that I also use [SourceTree](https://www.sourcetreeapp.com/) when reviewing code changes. So staging and commiting code from that GUI is not factored in, as well as bash history only recording the last 2000 lines.

Although there is a sizable list here the only ones I use on a day-to-day basis and recommend learning at minimum are:

- git status
- git checkout
- git pull
- git push
- git commit
- git add
- git merge
- git remote (maybe)



## Conclusion &#x1f481;&#x200d;&#x2642;&#xfe0f;

Essentially, in my opinion, this is **all** a junior developer needs to know to get by with Git. If you can learn the minimal commands and some grounding on some key features as mentioned, you should have enough to get by with Git. Anything else can be handled pragmatically and Googled when you encounter a problem. Even things like "merge conflicts" can be dealt with on the job and often requires direct communication with the team member, not necessary to practice in order to get started.

While this is a very basic introduction to Git and there are many advanced features of Git that wasn't included in this post.

But by applying the 80/20 rule, where 20% of the commands/features of Git will yield 80% of the results.

There are different Git workflows which would be good to learn but again, not mandatory and can be different depending on the team.
I've written a blog post about working with a particular Git workflow [here](/git-workflow)

Sure if you wanted to level up your Git knowledge and understand what other features it has, then of course feel free to learn them, my point is that, anecdotally, I've found that learning and even trying to remember those features you're not likely to use is not the best use of time, especially as a junior where that time can be used more effectively.

## Summary &#x1f4dd;

The reason I wanted to write this post was primarily to do with making it as simple to learn a topic as possible.

In my experience, when I've tried to learn something new, I find that I'm spending too much time on a topic and often never utilizing that knowledge. Git was a perfect example of this and having worked with it for a while I actually can serve up some data to prove my point.

I think I'll create more of these kinds of posts, not only to make it simple for anyone reading this, but to revisit some of the topics myself.

For fun, I also saw a few git typos in my `~/.bash_history` file, often occuring when I spam `git status`:
`git satus`, `git stat`, `git stattus`, `git staus`, `git statua`, `git stauts`, `git statu`, `git dif`, `git stasj`

&#x1f937;

### External sources &#x1f4a1;

[Git](https://git-scm.com/)

[Git Workflow (blog post)](/git-workflow)

[Wikipedia](https://en.wikipedia.org/wiki/Git)
