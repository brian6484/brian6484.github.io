---
date: 2022-03-07 14:35:23
layout: post
title: Difference between method size() and length()
description:
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
  - Head First Java
---

Perfectly answered here: https://stackoverflow.com/questions/20192843/difference-between-size-and-length-methods

size() is a method specified in java.util.Collection, which is then inherited by every data structure in the standard library. length is a field on any array (arrays are objects, you just don't see the class normally), and length() is a method on java.lang.String, which is just a thin wrapper on a char[] anyway.

> Perhaps by design, Strings are immutable, and all of the top-level Collection subclasses are mutable. So where you see "length" you know that's constant, and where you see "size" it isn't.






