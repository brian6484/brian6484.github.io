---
date: 2022-05-26 14:35:23
layout: post
title: Final keyword on variable, method and class
subtitle: Java 
description: Java
category: Java
tags:
  - Java
  - Head First Java
---

## Implications of final keyword
> A final variable means you can’t *change* its value.
> 
> A final method means you can’t *override* the method.
> 
> A final class means you can’ *extend* the class (i.e., you can’t make a
subclass)

If the class is final, you don’t need to mark the methods final. Think
about it—if a class is final, it can never be subclassed, so none of the
methods can ever be overridden.

On the other hand, if you do want to allow others to extend your class
and you want them to be able to override some, but not all, of the
methods, then don’t mark the class final, but go in and selectively mark
specific methods as final. A final method means that a subclass can’t
override that particular method.

