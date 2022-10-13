---
date: 2022-05-26 14:35:23
layout: post
title: Primitive and how to wrap and unwrap (feat. ArrayList<Object>)
subtitle: Java 
description: Java
category: Java
tags:
  - Java
  - Head First Java
---

## A note on primitive
Sometimes you want to treat a primitive like an object. For example,
collections like ArrayList only work with Objects:

There’s a wrapper class for every primitive type, and since the wrapper
classes are in the java.lang package, you don’t need to import them. You can
recognize wrapper classes because each one is named after the primitive
type it wraps, but with the first letter capitalized to follow the class naming
convention.

Class names: Boolean, Byte, Short, Long, Float, Double
Care **Characeter** and **Integer** as the names are not mapped
exactly to their primitive types. 

## Wrapping a primitive
> When you need to treat a primitive like an object, wrap it.


```java
int i= 20;
//give primitive to the wrapper constructor
Integer iWrap = new Integer(i);
```

<img src="/assets/images/posts/java/Primitive/1_primitive.png" title="제목" alt="아무거나" width="400"/>

## Unwrapping a value
```java
int unWrapped = iWrap.intValue();
```

## Java autobox(wrapps and unwraps) primitives automatically (feat ArrayList)
Compiler does it automatically for you!
