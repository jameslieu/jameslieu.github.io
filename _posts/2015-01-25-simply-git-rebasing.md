---
layout: post
title:  "Simply git-rebase"
date:   2015-01-25 23:00:00
categories: git-rebase git rebase
comments: true
---

Today I've decided to write about `Git Rebasing`.

<!--more-->

To be honest I've only recently discovered rebasing and I'm not too familiar with all of its uses or commands. What I do know is that the `git rebase` command allows me to modify the history of my repository by changing my `commits`. `Git rebase` can reorder, edit, or squash commits together. I've found this especially useful when commiting very minor changes such as removing white space or correcting typos. It happens all too frequently and these commits do nothing but clutter my repository history. Being able to combine those to a previous commit has made my commit history a lot cleaner.

Based on my experience I would typically use `git rebase` to:

- Delete commit messages or commits that are no longer necessary
- Squash multiple commits into one
- Edit my commit messages

Let me demonstrate an example with `git rebase -i HEAD~3`. Git rebase with the `-i` flag begins an interactive rebasing session. The `HEAD~3` flag refers to the latest commits with `~3` meaning how many commits or how far in my history I want to edit, in this case three commits.

This will then display the following:

<pre>
  pick 3dd14f1 second commit
  pick 0daba41 third commit
  pick f0111b0 fourth commit

  # Rebase 5376924..f0111b0 onto 5376924
  #
  # Commands:
  #  p, pick = use commit
  #  r, reword = use commit, but edit the commit message
  #  e, edit = use commit, but stop for amending
  #  s, squash = use commit, but meld into previous commit
  #  f, fixup = like "squash", but discard this commit's log message
  #  x, exec = run command (the rest of the line) using shell
  #
  # These lines can be re-ordered; they are executed from top to bottom.
  #
  # If you remove a line here THAT COMMIT WILL BE LOST.
  #
  # However, if you remove everything, the rebase will be aborted.
  #
  # Note that empty commits are commented out
  ~
  ~
  ~
</pre>

The top three lines represent my commits. `pick` being the command, following that is the commit identifier e.g.`3dd14f1` and finally your message e.g. `second commit`.

The rest are comments provided by `git` for additional information as indicated with a `#` at the start of the line. These are the commands that are available. However, I've only needed to use `pick`, `squash` and `fixup` thus far.

<pre>
  # Commands:
  #  p, pick = use commit
  #  r, reword = use commit, but edit the commit message
  #  e, edit = use commit, but stop for amending
  #  s, squash = use commit, but meld into previous commit
  #  f, fixup = like "squash", but discard this commit's log message
  #  x, exec = run command (the rest of the line) using shell
</pre>

Its always good to save certain changes or updates I make as I develop a feature or make additions to my codebase. Its a good habit to have, yet as I'm doing this, I would sometimes make two, three or even over five commits which represent the same feature. Therefore the commit messages are either very similar or will be too brief, which then can be confusing if read out of context.

This is would be a good time to `squash` my commits. `Squashing` commits essentially means combining my commit messages into one single commit which can therefore make more sense as a 'record' in my repository history. Sometimes I would need to look back on my respository history and it would be easier if the code or feature I'm looking for is located in a single commit as opposed to many smaller and unclear commits.

To `squash` my commits, I would have to select the commits I want to combine and use the `squash` command (leaving the `pick` command on the commit you want the other commits to 'combine' into).

<pre>
  pick 3dd14f1 second commit
  squash 0daba41 third commit
  squash f0111b0 fourth commit
</pre>

Once I make those changes and save. I would then be moved on to the next stage which then gives me the option to edit those messages if I wanted to. Which is great if I had typos or wanted to make my message more comprehensible, as an example I'll change the 2nd commit message to `Updated third commit`.

<pre>
  # This is a combination of 3 commits.
  # The first commit's message is:
  second commit

  # This is the 2nd commit message:

  Updated third commit

  # This is the 3rd commit message:

  fourth commit

  # Please enter the commit message for your changes. Lines starting
  # with '#' will be ignored, and an empty message aborts the commit.
  # rebase in progress; onto 5376924
  # You are currently editing a commit while rebasing branch 'master' on '5376924'.
  #
  # Changes to be committed:
  #       modified:   README.md
  #
  ~
  ~
  ~
</pre>
NOTE: Remember that these are the three latest commits as I used the `HEAD~3` flag

Save that and thats all there is to it! If I ran `git log` to see my current commits, I would only have two commits instead of four as both commit two, three and four are now `squashed` into a single commit and therefore makes my commit history cleaner and more organised.

<pre>
  james$ git log

  commit 73031c36716b6891dc1b7cd6304d156e369a515d
  Author: James Lieu <j.lieu888@gmail.com>
  Date:   Mon Jan 26 00:01:13 2015 +0000

      second commit

      Updated third commit

      fourth commit

  commit 537692465b7d350fb74870363e5abb3bbbb42ea7
  Author: James Lieu <j.lieu888@gmail.com>
  Date:   Mon Jan 26 00:00:58 2015 +0000

      initial commit
</pre>

When I add minor changes to my code such as removal of white spacing or new lines, they still need to be committed. This can be annoying if I have already made a commit before doing this. But having a commit message for those are unnecessary or irrelevant to my code/feature. This is where I can use the `fixup` command. The process is the same as `squashing`, meaning that the commits will be combined together. However, the commits that I use the `fixup` command on will then have its message removed.

NOTE: If you are performing a squash/fixup command on commits that have already been pushed to your remote repository your will have to `force` push your branch to the remote. For example, `git push -f origin master`

Another great git command is `git commit --amend`. This allows me to edit my last git message which is great for when I want a quick solution to fix typos or make changes to a commit I've just created.

This is the extent of my git rebasing experience so far, I have yet to find out what the other features of `git rebasing` does. Discovering these git techniques have made my commit history a lot more organised and cleaner. It also means less embarassing pull requests, espcially when I overlook something, fix typos and white spacing!
