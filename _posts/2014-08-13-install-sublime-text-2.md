---
layout: post
title:  "Install Sublime Text 2 in Ubuntu"
date:   2014-08-05 13:09:30
categories: sublime text ubuntu linux
comments: true
---

The fastest way I've found to install sublime text 2!

Copy and paste the following into the terminal
{% highlight ruby %}
  sudo add-apt-repository ppa:webupd8team/sublime-text-2
  sudo apt-get update
  sudo apt-get install sublime-text
{% endhighlight %}

After running this, Sublime Text 2 should have been installed within the /usr/lib/sublime-text-2 directory and can be launched from the Dashboard
Alternatively by typing <strong>subl</strong>, <strong>sublime-text</strong> or <strong>sublime-text-2</strong> into a Terminal window.
