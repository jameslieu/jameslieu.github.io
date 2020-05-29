---
layout: post
title:  "Autocomplete git commands and branch names"
categories: Programming
excerpt: In bash in Mac OS X, you can use TAB to autocomplete file paths. By default this doesn't work with git commands,  I'll have to manually configurate it
---

In bash in Mac OS X, you can use [TAB] to autocomplete file paths. By default this doesn't work with git commands,  I'll have to manually configurate it. Here's how:

Paste this command into the terminal, this will download the `git-completion.bash` script needed to execute the autocomplete:
<pre>
  curl https://raw.githubusercontent.com/git/git/master/contrib/completion/git-completion.bash -o ~/.git-completion.bash
</pre>

Next, add this to the `.bash_profile`. This line will tell bash to execute the git autocomplete script if it exists.

<pre>
  if [ -f ~/.git-completion.bash ]; then
    . ~/.git-completion.bash
  fi
</pre>

Restart bash and then autocomplete should work for git commands

If this doesn't work right off the bat, permission is probably needed to run the script:
<pre>
  chmod -X ~/.git-completion.bash
</pre>

When working in git I tend to come across or create long-winded git branch names so being able to autocomplete this will definietely improve my workflow.
