---
date: 2022-03-09 14:35:23
layout: post
title: Object Class polymorphism
subtitle: Java 
description: Java
category: Java
tags:
  - Java
  - Head First Java

---

## Every class in Java extends class Object

Class Object is the mother of all classes. It is the superclass of everything.
Every class you write extends Object.

Any class that doesn’t explicitly extend another class, implicitly extends
Object.

For example:
```java
public class Dog extends Object{
    
}
```

But wait a minute, Dog already extends something, Canine. That’s OK. The
compiler will make Canine extend Object instead. Except Canine extends
Animal. No problem, then the compiler will just make Animal extend Object.

## Object is a non-abstract class
Because it has method implementation code that all classes can inherit from and use, without
having to override them.

## SOME methods in Object can be overriden
Only some, but the rest are marked as *final*. Book encourages to override
hashCode(), equals() and toString().
