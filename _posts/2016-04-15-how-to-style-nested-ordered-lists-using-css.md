---
layout: post
title:  "How to style nested ordered lists using css"
date:   2016-04-15 23:51
categories: css
comments: true
---

I've found that it can be quite difficult to figure out how to style nested ordered lists using css. Imagine if I needed to put together a contract or Terms and conditions document using HTML and CSS.

<!--more-->

Its not uncommon for contracts to use sub sections and so the document will likely use nested ordered lists in HTML. What if the sub sections are styled differently?

An example can look something like this:

<div class='style-ol'>
  <ol>
    <li>
      Alpha
    </li>
    <li>
      Beta
    </li>
    <li>
      Charlie
    </li>
    <ol>
      <li>
        Delta
      </li>
      <li>
        Echo
      </li>
      <ol>
        <li>
          Foxtrot
        </li>
        <li>
          Golf
        </li>
        <li>
          Hotel
        </li>
      </ol>
    </ol>
  </ol>
</div>

In the example above, the first list style is numeric, the second are made up of letters and the third using roman numerals:

Here is my solution:

<pre>
  ol {
    counter-reset: first-counter;
    list-style-type: none;
    position: relative;
    padding-left: 20px;
    margin-left: 15px;
  }

  ol li {
    margin: 10px 0;
  }

  ol li:before {
    content: counter(first-counter) '.';
    counter-increment: first-counter;
    position: absolute;
    left: 0px;
  }

  ol ol {
    counter-reset: second-counter;
    list-style-type: none;
  }

  ol ol li {
    padding-left: 15px;
  }

  ol ol li:before {
    content: counter(second-counter, lower-alpha) '.';
    counter-increment: second-counter;
    list-style-type: none;
    left: 10px;
    position: absolute;
  }

  ol ol ol {
    counter-reset: third-counter;
  }

  ol ol ol li {
    padding-left: 15px;
  }

  ol ol ol li:before {
    list-style-type: none;
    content: counter(third-counter, lower-roman) '.';
    counter-increment: third-counter;
  }
</pre>

Firstly, you'll have to use `counter-reset`, and give it a sensible variable name e.g. `first-counter`, `second-counter` and `third-counter`.

<pre>
  ol {
    counter-reset: first-counter;
    list-style-type: none;
    position: relative;
    padding-left: 20px;
    margin-left: 15px;
  }
</pre>

I then set `list-style-type: none;`, which pretty much removes the original list style completely

<pre>
  ol li:before {
    content: counter(first-counter) '.';
    counter-increment: first-counter;
    position: absolute;
    left: 0px;
  }
</pre>

Then in the psudo-element `:before`, append the content style:

`content: counter(first-counter)`
('first-counter' is the variable you declared earlier)

Increment using `counter-increment`. Then you'll need to use the `position` style to adjust the position accordingly.

To change the list style type you can pass that in as a second argument
`content: counter(second-counter, lower-alpha) '.';`

<pre>
  a. foo
  b. bar
  c. baz
</pre>

And finally, if I wanted to change the character (decimal point) after the list-style, all I have to do is change the string: `content: counter(first-counter) '%';`

<pre>
  1% foo
  2% bar
  3% baz
</pre>

As you can see, this is extremely hacky and as far as I can tell, seems to be the only way you can style nested ordered lists.

In any case, it felt great to have finally found the solution, and I'll definitely be refering to this post next time I'm asked to style ordered lists.
