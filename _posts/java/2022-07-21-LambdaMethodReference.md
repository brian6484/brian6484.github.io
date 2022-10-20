---
layout: post
title: Java Stream operation methods with examples
subtitle: Java 
description: Java
category: Java
tags:
  - Java
  - Head First Java

## Sometimes don't even need lambda via **method reference**
Following up with my previous [StreamLambda post](https://brian6484.github.io/java/2022/06/13/Lambda.html)
Let's look at the previous lambda expression for map operation

```java
Function<Song,String> getGenre = song->song.getGenre();
```

Instead of spelling this whole thing out, you can point the compiler to a
method that does the operation we want, using a method reference.

<img src="/assets/images/posts/java/MethodReference/methodref1.png" title="제목" alt="아무거나" width="400"/>
