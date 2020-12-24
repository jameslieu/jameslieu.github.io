---
layout: post
title: "Pointers in Go (Golang)"
categories: Programming
excerpt: What is a Pointer?
---

<img src="/assets/media/pointers-in-go-1.jpeg" style="height:200px; margin: auto">
I'm learning a little bit of Go (Golang). There are a few areas in this programming language which are familiar to me and there are many areas which are not.
One of which are Pointers.

## What is a Pointer? &#x1f449;

A pointer is a variable that stores the address of a value, rather than the value itself. If you think of a computer's memory (RAM) as a JSON object, a pointer would be like the key and a normal variable would be the value.

```
{
  "pointer": "variableValue"
}
```

## Syntax

### Creating a Pointer: &#x1f968;

To create a pointer variable, you prefix your value with an ampersand (`&`)

```
someString := ""
someStringPointer := &someString
```

If you print that pointer you will see a memory address.
```
package main

import "fmt"

func main() {
  someString := "some string"
  someStringPointer := &someString
  fmt.Println(someStringPointer)
}

```
This will print something that looks like this: `0xc00000e1e0`, Which is the memory address of that variable in your machine.

### Describing a pointer: &#x2733;

In a function signature or type definition, the asterisk or `*` is used to designate that a value is a pointer.

```
func PassPointer(pointer *string) {
}
```

### Modify the original variable: &#x2733;

You can use the `*` to modify the value of the original variable which the pointer references

```
someString := "some value"
someStringPointer := &someString
*someStringPointer = "new value"
fmt.Println(someString)
}

// Prints "new value"
```

The `someString` variable will now equal: `new value`.

## When Should Pointers Be Used &#x1f937;

These are the reasons I've read where you might want to use a pointer:

### &#x1f91d; A function that mutates one of it's parameters

When calling a function that takes a pointer as an argument and expect that the variable will be mutated. If the variable doesn't need to be mutated then a pointer probably wouldn't need to be used

### &#x23f1; Better performance

If you have a large string in memory, it can be very expensive to copy that variable each time it is passed to a new function. It may be worthwhile to pass a pointer instead to save CPU and memory

### &#x1f919; Need a Nil value option
Sometimes a function needs to know what something's value is, as well as if it exists or not. For example, if a JSON object is:

```
{ "name": "James" } // *name: "James"
{ "name": "" }      // *name: ""
{}                  // *name: nil
```

These are the ones I know of so far, I'm sure there are other uses I'm not aware of.

## Summary &#x1f4dd;

There is no passing by reference in Go. So pointers are a way to do this if required. There are probably more benefits to using pointers that I haven't mentioned, but I've only just started learning all of this very recently.

It seems that working with normal values are usually fine, and from what I've read about pointers, it ok to avoid them generally speaking. They may be useful tools if used effectively but can easily lead to unreadable code and make it difficult to debug.