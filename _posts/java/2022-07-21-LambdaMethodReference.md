---
layout: post
title: Method reference to replace lambda expressions
subtitle: Java 
description: Java
category: Java
tags:
  - Java
  - Head First Java
---
## Sometimes don't even need lambda via **method reference**
Following up with my previous [StreamLambda post](https://brian6484.github.io/java/2022/06/13/Lambda.html)
Let's look at the previous lambda expression for map operation

```java
Function<Song,String> getGenre = song->song.getGenre();
```

Instead of spelling this, you can point the compiler to a
method that does the operation we want, using a method reference.

<img src="/assets/images/posts/java/MethodReference/methodref1.png" title="제목" alt="아무거나" width="400"/>

## Example of method reference
For example, Comparator! There are a lot of helper
methods on the Comparator interface that, when combined with a method
reference, let you see which value is being used for sorting and in which
direction. 

To sort songs from oldest to newest with lambda:
```java
List<Song> result = allSongs.stream()
  .sorted((o1,o2)->o1.getYear()-o2,getYear())
  .collect(toList());
```

But with method reference with Comparator's **static** helper method:
```java
List<Song> result = allSongs.stream()
  .sorted(Comparator.comparingInt(Song::getYear))
  .collect(toList());
```

More on static helper method

