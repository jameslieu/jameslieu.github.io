---
layout: post
title:  "Launch Sublime Text 3 using command line"
categories: Tooling
excerpt: Sublime Text 3 ships with a CLI called `subl`. You will have to do a minor configuration though.
---

Sublime Text 3 ships with a CLI called `subl`. You will have to do a minor configuration though.

Firstly, check your `$PATH` by running: `echo $PATH`.

It should look like this:
`/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin`

Then copy this into terminal:

`ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin/subl`

Now typing `subl` in the command line should open Sublime
