---
date: 2022-03-01 14:35:23
layout: post
title: Encapsulation in Java
subtitle: Java 
description: Java
category: Java
tags:
  - Java

1. Encapsulation in Java

 * Without encapsulation, we can access and manipulate instance variables.
 * Encapsulation's rule of thumb is to mark *instance variables private* and *getters and setters as public*.
 * Through encapsulation, instance variables are protected via forcing code through setters. That way, the
   setter method can validate the parameter and decide if it’s durable. Maybe the
   method will reject it and do nothing, or maybe it’ll throw an Exception (like
   if it’s a null Social Security number for a credit card application), or maybe
   the method will round the parameter sent in to the nearest acceptable value.
 * How about setter methods that just set the value of instance variables. Doesn't that just place unnecssasry overhead?
 * No, because The point to setters (and getters, too) is that you can change your
   mind later, without breaking anybody else’s code!
 * 

