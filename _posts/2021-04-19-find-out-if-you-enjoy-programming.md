---
layout: post
title: "Find Out If You Enjoy Programming"
categories: Programming
excerpt: What would be the fastest way for someone who has no programming experience to find out whether they would enjoy it or not?
---

<iframe width="560" height="315" src="https://www.youtube.com/embed/RN8ZXxq2awQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

In many ways, the point of programming is to use a computer to solve problems. Pretty much every code a developer writes involves problem solving in one form or another, do they need to automate a process? Fetch data from somewhere? to store data into a database? How would they achieve this?

All of these involve solving a problem, and it is this problem solving process which appears to make programming enjoyable for developers.

With this in mind, what would be the fastest way for someone who has no programming experience to find out whether they would enjoy it or not?

## Why Do Devlopers Enjoy It?

I've Googled "why do developers love coding". And you can see developers respond with answers such as:

1. Puzzles and Problem solving
2. Creating something amazing from scratch
3. The sheer joy of making things, Programming is fundamentally about creating solutions to problems.
4. Converting ideas / imaginations into reality
5. The pleasure of making things that are useful to other people
6. Programming improves our problem solving skills.
7. Liking coding because they like puzzles and makes their lives easier

These are some of the answers I've seen and agree with personally. Things like

- Having a strong sense of purpose or accomplishments
- The satisfaction of finding solutions to problems
- The constant learning and the option of learning different languages, frameworks or technologies

Altogether, these reasons to me can be boiled down to two primary reasons why programming is enjoyable.

### Learning And Problem Solving

So in my opinion, the fastest way to first find out whether somebody will enjoy this is to choose a beginner friendly programming problem or exercise to solve, and needs to have utilize a number of features of programming combined to solve it.

## Prerequisites

Ideally they would be following this exercise on their computer, the point is for them to actually follow and do the exercise to determine whether they'll enjoy programming or not.

So if I were somebody who was unsure about whether I'll be interested in this, I would want the least barrier to entry. So here are some prerequisites I think will help with that.

### No installation required
There should be no downloading or installing programming languages to your computer

### No programming knowledge required

They also wouldn’t need any experience with programming yet as I’ll run through the very basics and exactly what they would need to know in order to complete the short exercise.

And so to meet this requirement, the programming language I have chosen for this exercise is **JavaScript**

The main reason is that it’s a good beginner friendly language, and because most web browsers support it, you wouldn’t need to download anything in order to get started.

Ok so I’ll begin by going though, specifically the javascript basics needed to solve the exercise.

## The Basics

### Strings

```javascript
// Strings are created with ' or ".
'abc';
"Hello, world";
"01/01/2001";
```

In computer programming, a string is a data type, and is basically a sequence of characters. They are created with a single quote or double quote. And in layman’s terms, you can use them to construct words or other sequences of characters.

### Integers

```javascript
// integers are whole numbers
123

// Some basic arithmetic works as you'd expect.
1 + 1; // = 2
8 - 1; // = 7
10 * 2; // = 20
35 / 5; // = 7
```

Integers are whole numbers. And basic arithmetic works as you’d expect.

###  Variables

```javascript
let teamName = ‘Foobar’;
let numberOfCars = 5;

const gameName = ‘tic tac toe’;
const rows = 9;

var fullName = ‘John Doe’;
var age = 50;
```

Computer programs use variables to store information. Any data type can be stored in a variable for example, a person’s name, their age, date of birth.

You can assign a variable using either the `var`, `let` or `const` keyword.

It is preferred to use either the `const` or `let` keyword. `Const` for when you don’t need to reassign this variable, and `let` for when you do.

Avoid using `var`

### Boolean

```javascript
let isActive = true;
let isDisabled = false;
```

In computer science, Boolean is a data type that has one of two possible values (usually denoted true and false)

### Comparison Operators

```javascript
// Equality is ===
1 == 1; // = true
2 == 1; // = false

// Inequality is !==
1 != 1; // = false
2 != 1; // = true

// More comparisons
1 < 10; // = true
1 > 10; // = false
2 <= 2; // = true
2 >= 2; // = true
```

These are used in logical statements to determine equality, inequality or difference between values. When using comparison operators, it’s “return type” is a boolean.

For example, `1 == 1` is `true`,  and `2 == 1` is `false`
To compare whether something is NOT equal to something, use the exclamation mark followed by the equals character.

And other comparison operators are  less than, more than, less than or equal to OR more than or equal to.

### Concatenation

```javascript
// Strings are concatenated with +
"Hello " + "world!"; // = "Hello world!"

// ... which works with more than just strings
"1, 2, " + 3; // = "1, 2, 3"
```

Strings and or numbers can be concatenated by using the plus operator. Think of it as combining two values together

### Conditional Statements

```javascript
var count = 1;
if (count == 3){
    // evaluated if count is 3
} else if (count == 4){
    // evaluated if count is 4
} else {
    // evaluated if it's not either 3 or 4
}
```

conditional statements, or if / else statements are used to perform actions based on certain conditions.

To use these statements, use the `if` keyword followed by your condition in parenthesis which needs to be a boolean value,

In this example, if the count equals 3 then the block directly underneath will be evaluated, else if count is equal to 4 then the block underneath that will be executed, and if neither of those are true then the following else statement will be executed.

You can also use the `if` statement without any preceding `else` statements, if the condition isn’t met, then the logic within its block will not be executed.

### Loops

```javascript

for (var i = 0; i < 5; i++){
    // will run 5 times
}

while (true){
    // An infinite loop!
}

```

So loops are used to execute a block of statement, a specified number of times, OR till a specified condition is true.

The one we’re using for this exercise is **the while loop**

So, the While Loop is used to, execute a block of statements, till a specified condition is true, if the condition becomes false the While Loop terminates.

We do need make sure we have a way to break out of the loop, otherwise we could end up with an infinite loop and crash the program.

### console.log

```javascript
const gameName = ‘tic tac toe’;
console.log(gameName); // tic tac toe
```

## The Exercise

Print the lyrics for the [99 bottles of beer](http://99-bottles-of-beer.net/lyrics.html) song into the console.

The lyrics are very repetitive, where it counts from 99 bottles of beer down to 0 bottles of beer. As shown in the javascript basics, you might already be able to picture how you would solve this.

I've created a video which goes through the exercise.

<iframe width="560" height="315" src="https://www.youtube.com/embed/RN8ZXxq2awQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

In my tutorial, although there were a few steps to achieve the outcome, ultimately there were two actions in play.

The first was learning something new, programming basics such as strings, integers, conditional operators and loops.

The second was to use those programming tools in order to solve a problem, in our case it was to first print a countdown of the number of bottles on the wall in the console

A Beginner level challenge, but the process of discovering and solving those problems is what we should pay attention to. If you were bored of breaking down the problem into steps and eventually solving it then programming is probably not for you.

Try other programming challenges or refining this existing one, try different loops such as the "while" or "do while" loop and see if you can achieve the same result.

However, if you did enjoy completing the task and seeing your results onto the console, then perhaps programming could be enjoyable and may be something you should consider learning and even pursue a career in.

Here is the solution to the problem

```javascript
let word = 'bottles';
let count = 99;

while (count >= 2) {
    if (count == 2) {
        word = 'bottle';
    }
    let prev = count - 1;
    console.log(count + " bottles of beer on the wall, " + count + " bottles of beer, Take one down, pass it around, " + count + " " + word +  " of beer on the wall.");
    count = count - 1;
}
console.log("1 bottle of beer on the wall, 1 bottle of beer. Take one down and pass it around, no more bottles of beer on the wall.");
console.log("No more bottles of beer on the wall, no more bottles of beer. Go to the store and buy some more, 99 bottles of beer on the wall.");
```

## Summary &#x1f4dd;

Often I see people ask about whether they should become software developers or make the leap and switch careers and pursue one in programming. In this career and like many others, it really helps if you enjoy it.

And when curious or interested about a new topic or leisure, you can only really find out if it's something you'd enjoy by getting "hands-on" and trying it out.

It can be daunting to see the many different ways of learning or getting started, but in my experience, just learning the basics on it's own isn't as interesting or enjoyable. It's only when you apply those basics and fundamentals to something do you really start to discover whether it's something you can enjoy or not.