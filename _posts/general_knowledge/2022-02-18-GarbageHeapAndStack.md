---
date: 2022-02-18 14:35:23
layout: post
title: The Stack and the Heap: where things live
description:
category: General Knowledge
tags:
  - General Knowledge
  - Head First Java
---

숨참고 love dive~

## Introduction
When a JVM starts up, it gets
a chunk of memory from the underlying OS and uses it to run your Java
program. How much memory, and whether or not you can tweak it, is
dependent on which version of the JVM (and on which platform) you’re
running.

## The Stack and the Heap

Basically, area of memory where **all** *objects* live in
(the heap), method invocations and local variables (not instance 
variables that are declared in class) live in
(the stack).

### Stack

<img src="/assets/images/posts/General_Knowledge/12_stack1.png" title="제목" alt="아무거나" width="400"/> 

>The method on the top of the stack is always the currently executing
method.

When you call a method, the method lands on the top of a call stack. That
new thing that’s actually pushed onto the stack is the stack *frame*, and it holds
the state of the method including which line of code is executing, and the
values of all local variables.

The method at the top of the stack is always the currently running method for
that stack (for now, assume there’s only one stack, but in Chapter 14, A Very
Graphic Story, we’ll add more.) A method stays on the stack until the
method hits its closing curly brace (which means the method’s done). If
method foo() calls method bar(), method bar() is stacked on top of method
foo().


### Heap
All *objects* live on the garbage-collectible heap

## What about local variables that are *objects*?
Non-primitive variable holds a reference to an object, not the
object itself.

>If the local variable is a
reference to an object, only the variable (the reference/remote control)
goes on the stack.

<img src="/assets/images/posts/General_Knowledge/13_stack2.png" title="제목" alt="아무거나" width="400"/> 

## Then, where do instance variables live?

As mentioned, local variables live in the stack. But what about
instance variables?

When we create a new object CellPhone(), Java makes space on the
Heap for that. The space allocated is enough for the object,
which means enough to house all the object's instance variables.

> Instance variables (specifically the *values of object's instance variables) live on the Heap, *inside* the object they belong to.

If instance variables are all primitives, Java makes space for the
variables based on the primitive type. E.g. int needs 32 bits,
long need 64 bits, etc. Java doesn’t care about the value inside primitive variables; the
bit-size of an int variable is the same (32 bits) whether the value of the int is
32,000,000 or 32.

### What if instance variables are *objects*?

E.g. What if CellPhone HAS-A
Antenna? In other words, CellPhone has a reference variable of type
Antenna.

When the new object has instance variables that are object references rather
than primitives, the real question is: does the object need space for all of the
objects it holds references to? 

NO! No matter what,
Java has to make space for the instance variable values. But remember that a
reference variable value is not the whole *object*, but merely a *remote control*
to the object. So if CellPhone has an instance variable declared as the non-primitive type Antenna, Java makes space within the CellPhone object only
for the Antenna’s *remote control* (i.e., reference variable) but not the
Antenna *object*.

Antenna object gets space on the Heap unless or until reference
variable is assigned a new Antenna object.

```java
    private Antenna ant = new Antenna();
```










