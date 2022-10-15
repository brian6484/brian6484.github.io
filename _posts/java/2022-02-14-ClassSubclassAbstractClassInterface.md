---
date: 2022-02-14 14:35:23
layout: post
title: How to differentiate class, a subclass, an abstract class or an interface?
subtitle: Java 
description: Java
category: Java
tags:
  - Java
  - Head First Java
---
When to differentiate these 4:

* Make a class that doesn’t extend anything (other than Object) when your
new class doesn’t pass the IS-A test for any other type.


* Make a subclass (in other words, extend a class) only when you need to
make a more specific version of a class and need to override or add
new behaviors


* Use an abstract class when you want to define a **template** for a group of
subclasses, and you have at least *some* implementation code that all
subclasses could use. Make the class abstract when you want to
guarantee that nobody can make objects of that type.


* Use an interface when you want to define a *role* that other classes can
play, regardless of where those classes are in the inheritance tree.

