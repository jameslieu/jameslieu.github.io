---
layout: post
title:  "What is Polymorphism?"
date:   2014-12-29 17:07:00
categories: polymorphism
comments: true
---

<b>What is polymorphism?</b>

<img src="/assets/media/polymorphism_example.png" />

What is polymorphism? I've found that this question in particular is asked quite frequently in tech interviews. I was asked this in a phone interview once and I did not know the answer to this unfortunately. I believe that it was this question that prevented me from getting to the next stage of the interview, so of course I decided to look into it.

Polymorphism essentially means <em>many forms</em> and is one of the fundamental features of object oriented programming. It lets us automatically do the correct behavior even if what we're working with could take one of many different forms, simply put; it means being able to send the same massage and get different results. Here's the most basic example I've found; the <strong>+</strong> operator.

In Ruby the <strong>+</strong> operator will <em>behave</em> differently depending on how you use it.

For example, lets say you have two variables; <strong>a</strong> and <strong>b</strong>.

If the two variables are <strong>numbers</strong>, the <strong>+</strong> operator will numerically add them.
{% highlight ruby %}
a = 1
b = 2

a + b
=> 3
{% endhighlight %}

However, what if the two variables were <strong>strings</strong> instead?
{% highlight ruby %}
a = "Hello "
b = "World"

a + b
=> "Hello World"
{% endhighlight %}

As you can see, using <strong>+</strong> operator for <strong>strings</strong> will <em>concatenate</em> them instead.

Now this is a basic example of how polymorphism works and is built into a lot of programming languages, but we can use the same idea with our own classes and objects.

----
Here is an example of a polymorphic association:

{% highlight ruby %}

class Animal
    
    def make_noise 
        "Some noise"
    end

    def sleep 
        puts "#{self.class.name} is sleeping." 
    end
  
end

class Dog < Animal
    
    def make_noise 
        'Woof!'         
    end 
    
end

class Cat < Animal 
    
    def make_noise 
        'Meow!' 
    end 
end

{% endhighlight %}


Lets say we have a simple inheritance hierarchy. There is an <strong>Animal</strong> superclass and two descendant subclasses, a <strong>Cat</strong> and a <strong>Dog</strong>. Each of these three classes has its own implementation of the <em>make_noise</em> method. The implementation of the method of the descendants replaces the definition of a method in the <strong>Animal</strong> class.

{% highlight ruby %}
class Dog < Animal
    
    def make_noise 
        'Woof!'         
    end 
    
end
{% endhighlight %}

The <em>make_noise</em> method in the <strong>Dog</strong> class replaces the <em>make_noise</em> method of the <strong>Animal</strong> class. The idea is that even though the <strong>Dog</strong> class is <em>inheriting</em> from the <strong>Animal</strong> class and would therefore already have access to the <em>make_noise</em> method, the <strong>Dog</strong> class will have its own <em>specialized</em> version of that method which is unique to that particular class. This is referred to as overiding the method of the superclass, which just means you write it again.

This means is that the method will change its behaviour depending where it was originally instantiated from. Now you may wonder why this would be useful.. Here is an example:

{% highlight ruby %}

[Animal.new, Dog.new, Cat.new].each do |animal|
  puts animal.make_noise
end

=>
Some noise
Woof!
Meow!

{% endhighlight %}

If you had an array of <strong>Animal</strong>, <strong>Dog</strong> or <strong>Cat</strong> objects as shown above, you can call the <em>make_noise</em> method on all of them and it will return the <strong>correct</strong> output as expected. While this is a relatively simplified example, you can see why this would be useful if we had an array of a thousand of these objects. We won't need to look into where they were originally instantiated from, we just know that it works.
