---
layout: post
title:  "SSH Cheat Sheet"
date:   2014-08-05 13:09:30
categories: ssh
comments: true
---

SSH otherwise know as Secure Shell is a protocol that allows data to be transferred securely between two networked devices. To put it simply, it’s a way of connecting to and using another machine either next to you, or the other side of the world securely.

I've found these commands to be very useful at at the same time I can just as easily forget them. Therefore in this post I wanted to add a cheat sheet so I can refer back to it whenever I need to. If there are any you think will also be useful please let me know in the comments below.

---

### Exploring a directory
To look at the current directory:
{% highlight ruby %}
  ls
{% endhighlight %}
{% highlight ruby %}
  ls -la
{% endhighlight %}

To change directory:

{% highlight ruby %}
  cd pathname/directory/subdirectory
{% endhighlight %}

Or to go up a level:
{% highlight ruby %}
cd ../
{% endhighlight %}
Or you can chain these commands together:
{% highlight ruby %}
cd ../../themes/images
{% endhighlight %}

---

### Copy a file
To copy a file with the same directory simply type:

{% highlight ruby %}
cp filename-to-copy.txt new-file-name.txt
{% endhighlight %}

For example:
{% highlight ruby %}
cp index.html index.back.html
{% endhighlight %}

To copy between directories:

{% highlight ruby %}
cp filename.txt ../../new-directory/filename.txt
{% endhighlight %}

For example

{% highlight ruby %}
cp contact.php ../contact/contact.php
{% endhighlight %}

To copy all files from one directory to another, use the * character, which unofficially means all:

{% highlight ruby %}
cp images/* ../skin/
{% endhighlight %}

---

### Move a file
To move a file simply type:
{% highlight ruby %}
mv current-directory/file.txt ../new-directory/file
{% endhighlight %}

For Example:
{% highlight ruby %}
mv images/image.jpg ../docs/
{% endhighlight %}

---

### Rename a file
To rename a file, use the ‘mv’ but change the name of the file when stating the directory receiving the file.
{% highlight ruby %}
mv oldfilename.txt newfilename.txt
{% endhighlight %}

For Example
{% highlight ruby %}
mv index.php index.bac.php
{% endhighlight %}

---

### Delete a file
To delete a file type:
{% highlight ruby %}
rm filename.txt
{% endhighlight %}
Alternatively if you wish to delete a directory, and all directories and files within that recursively, type:
{% highlight ruby %}
rm -r
{% endhighlight %}

---

