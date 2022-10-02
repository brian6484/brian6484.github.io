---
date: 2022-01-07 14:35:23
layout: post
title: How does Java code run? (feat. Compiler & JVM)
description:
category: General Knowledge
tags:
  - General Knowledge
  - Head First Java
---
I only heard about compilers and JVMs but did not know for sure what they were,
and how they relate to help run Java code.

## Compiler:

Run your source code through compiler and it checks for errors. It won't compile until
it is satisfied that everything will run correctly. Checks variables of wrong type that
stops majority of errors.

But some still get through to JVM, like *ClassCastException* or other datatype exceptions that
emerge at runtime. But this is to support one of Java’s other important features —dynamic
binding. At runtime, a Java program can include new objects that weren’t even known to the original programmer, 
so it has to allow a certain amount of flexibility. But it can stop anything that would
never-could never—succeed at runtime.

Head-first java states that 
> "Excuse me, but I am the first line of defense, as they say. The datatype
violations I previously described could wreak havoc in a program if
they were allowed to manifest. I am also the one who prevents access
violations, such as code trying to invoke a private method, or change a
method that—for security reasons—must never be changed. I stop
people from touching code they’re not meant to see, including code
trying to access another class’ critical data."

It then creates a new document, coded into Java **bytecode**. This compiled bytecode is platform-independent.

## JVM (Java virtual machine):

Reads and runs this bytecode













