---
layout: post
title:  "Launch Sublime Text 3 using command line"
date:   2015-10-04 13:35:00
categories: sublime
comments: true
---

Sublime Text 3 ships with a CLI called `subl`. You will have to do a minor configuration though.

<!--more-->

Firstly, check your `$PATH` by running: `echo $PATH`.

It should look like this:
`/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin`

Then copy this into terminal:

`ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin/subl`

Now typing `subl` in the command line should open Sublime
