---
date: 2022-02-10 14:35:23
layout: post
title: Interface
subtitle: Java 
description: Java
category: Java
tags:
  - Java
  - Head First Java
---

## Introduction & Deadly Diamond of Death (DDD)

From pg 565 of Head First Java gives reason to why inheritance is useful.

Deadly Diamond of Death (DDD) arises from 2 superclasses (multiple inheritance) where
a subclass does not know which method to use, that is declared the same in both
superclasses.

## Interface

A Java interface solves your multiple inheritance problem by giving you
much of the polymorphic benefits of multiple inheritance without Deadly Diamond of Death (DDD).

The solution is to simply:
> make all methods abstract!

That way, the subclass must implement the
methods (remember, abstract methods must be implemented by the first
concrete subclass), so at runtime the JVM isn’t confused about which of the
two inherited versions it’s supposed to call.

## DEFINE an interface

1) Say "interface" instead of "class".

2) Interface methods are *implicityly* public and abstract so typing in "public" and
"abstract" is optional. And it is not good to type those words in but just to show you,
they were added

3) All interface methods are abstract, so they do not have a body and end in semicolons

```java
public interface Pet{
    public abstract void beFriendly();
    public abstract void play();
}
```
## Implement an interface
1) "implements" keyword with the name of the inteface
2) implement the abstract interface methods (e.g. Pet methods)

```java
public class Dog extends Canine implements Pet{
    public void beFriendly(){
        //implement pet methods blabla
    }
    public void play(){
        //implement pet methods bla bla
    }
    
    //regular Animal methods to be overriden
    public void roam(){
        //blabla
    }
}
```

## More on interface
>Classes from different inheritance trees can implement the same
interface

When you use a class as a polymorphic type (like an array of type Animal or
a method that takes a Canine argument), the objects you can stick in that type
must be from the same inheritance tree. But not just anywhere in the
inheritance tree; the objects must be from a class that is a subclass of the
polymorphic type. An argument of type Canine can accept a Wolf and a Dog,
but not a Cat or a Hippo.

But when you use an interface as a polymorphic type (like an array of Pets),
the objects can be from anywhere in the inheritance tree. The only
requirement is that the objects are from a class that implements the interface.
Allowing classes in different inheritance trees to implement a common
interface is crucial in the Java API. Do you want an object to be able to save
its state to a file? Implement the Serializable interface. Do you need objects
to run their methods in a separate thread of execution? Implement Runnable.
You get the idea. You’ll learn more about Serializable and Runnable in later
chapters, but for now, remember that classes from any place in the
inheritance tree might need to implement those interfaces. Nearly any class
might want to be saveable or runnable.

> Class can implement MULTIPLE intefaces!

Roses are red, Violets are blue. Extend only one, but implement two.

Single parents only! A Java class can have only 1 parent (superclass) and that
parent class defines who you are. But you can implement multiple interfaces that 
define roles that you can play.

## Summary
>A Java interface is like a 100% pure abstract class.
