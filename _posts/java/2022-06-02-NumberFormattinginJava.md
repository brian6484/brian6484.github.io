---
date: 2022-06-02 14:35:23
layout: post
title: How to format numbers in Java (feat "%")
subtitle: Java 
description: Java
category: Java
tags:
  - Java
  - Head First Java
---

## Format specifier
A format specifier can have up to five different parts (not including the
“%”). Everything in brackets [ ] below is optional, so only the percent
(%) and the type are required. But the order is also mandatory, so any
parts you DO use must go in this order.

<img src="/assets/images/posts/java/Number/1_number.png" title="제목" alt="아무거나" width="400"/>

> Btw, although type is the only required specifier, remember that if you do put in
anything else, type must always come last! 

<img src="/assets/images/posts/java/Number/2_number.png" title="제목" alt="아무거나" width="400"/>

For example, 
```java
int one = 100000;
double two = 100000.2489;
String s = String.format("Rank is %,d out of %,.2f",one, two);
//output is :Rank is 100,000 out of 100,000.25
```
