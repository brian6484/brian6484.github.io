---
date: 2022-03-06 14:35:23
layout: post
title: Inheritance
subtitle: Java 
description: Java
category: Java
tags:
  - Java
  - Head First Java

Inheritance:

## Introduction
<img src="/assets/images/posts/3_inheritance.png" title="제목" alt="아무거나"/> 

Subclass (square, triangle, etc) inherits from the superclass (shape). Subclass can
override methods but instance variables are not overridden because they don’t need to be. They
don’t define any special behavior, so a subclass can give an inherited
instance variable any value it chooses. PantherMan can set his inherited
tights to purple, while FriedEggMan sets his to white.

Subclass can add new instance variables and methods apart from those inhertied from
superclass. A subclass inherits all **public** instance variables and methods of the
superclass, but does not inherit the **private** instance variables and
methods of the superclass.

In Java, we say that the subclass **extends** the superclass. An inheritance
relationship means that the subclass inherits the members of the superclass.
When we say “members of a class,” we mean the *instance variables* and
*methods*.

## IS-A test:

The IS-A test should make sense when you ask any subclass  if it IS-A any of its supertypes.
If class B extends class A, class B IS-A class A.
This is true anywhere in the inheritance tree. If class C extends class B,
class C passes the IS-A test for both B and A.

For example, 
Canine extends Animal
,Wolf extends Canine
,Wolf extends Animal
,Canine IS-A Animal
,Wolf IS-A Canine
,Wolf IS-A Animal

You’re always allowed to say “Wolf extends Animal” or “Wolf IS-A Animal.” It makes no
difference if Animal is the superclass of the superclass of Wolf. In fact, as long as
Animal is somewhere in the inheritance hierarchy above Wolf, Wolf IS-A
Animal will always be true.

Superclass cannot extend subclass/inherit from subclass. There’s no reverse or
backward inheritance. Think about it, children inherit from parents, not
the other way around.

## In subclass, use both superclass and overriding subclass version

Head First Java explains really well:

<img src="/assets/images/posts/4_inheritance_super.png" title="제목" alt="아무거나"/> 

## When to use inheritance?
1) When one class is a more specific type of a superclass.
   Example: Willow is a more specific type of Tree, so Willow extends Tree
   makes sense.
2) Have behavior (implemented code) that
   should be shared among multiple classes of the same general type. Example:
   Square, Circle, and Triangle all need to rotate and play sound, so putting that
   functionality in a superclass Shape might make sense and makes for easier
   maintenance and extensibility.

## When NOT to use inheritance?
1) just so that you can reuse code from another class,
   if the relationship between the superclass and subclass violate either of the
   above two rules. For example, imagine you wrote special printing code in
   the Animal class and now you need printing code in the Potato class. You
   might think about making Potato extend Animal so that Potato inherits the
   printing code. That makes no sense! A Potato is not an Animal! (So the
   printing code should be in a Printer class that all printable objects can take
   advantage of via a HAS-A relationship.)
2) DO NOT use inheritance if the subclass and superclass do not pass the IS-A
   test. Always ask yourself if the subclass IS-A more specific type of the
   superclass. Example: Tea IS-A Beverage makes sense. Beverage IS-A Tea
   does not.





