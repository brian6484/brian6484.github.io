---
layout: post
title: Java's Exception handling
subtitle: Java 
description: Java
category: Java
tags:
  - Java
  - Head First Java

## Intro
So, how does a method tell you it might throw an exception? You find a
**throws** clause in the risky method’s declaration.

> Risky methods that could fail at runtime declare the exceptions that might happen using
“throws SomeKindOfException” on their method declaration.

## Try-catch to catch the exception
<img src="/assets/images/posts/java/Exception/exception1.png" title="제목" alt="아무거나" width="400"/>

Basically, I am gonna **TRY** this risky thing, and I will
**CATCH** myself if it fails.

A try/catch block tells the compiler that you know an exceptional thing could
happen in the method you’re calling, and that you’re prepared to handle it.
That compiler doesn’t care how you handle it; it cares only that you say
you’re taking care of it.

## Exception is an **object** of type Exception
Everything in Java is an object remember? Even exceptions.

Remember polymorphism's property so
an object of type Exception can be an instance of any **subclass** of Exception.

<img src="/assets/images/posts/java/Exception/exception3.png" title="제목" alt="아무거나" width="400"/>

Because an Exception is an object, what you catch is an object. In the
following code, the catch argument is declared as type Exception, and the
parameter reference variable is e.

<img src="/assets/images/posts/java/Exception/exception2.png" title="제목" alt="아무거나" width="400"/>

## If it’s your code that catches the exception, then whose code throws it?

You’ll spend much more of your Java time handling exceptions than
creating and throwing them yourself. For now, just know that
when your code calls a risky method —a method that declares an exception—
it’s the risky method that throws the exception back to you, the caller.

In reality, it might be you who wrote both classes. It really doesn’t matter
who writes the code...what matters is knowing which method throws the
exception and which method catches it.

When somebody writes code that could throw an exception, they must
declare the exception too!


