---
date: 2022-01-07 14:35:23
layout: post
title: Difference between Array and ArrayList
description:
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
  - Head First Java
---
1) A regular array has to be declared its size upon creation. But for ArrayList, just need to 
make an object of type ArrayList. You can actually give initial size to ArrayList too.
```java
int[] myList = new int[];
ArrayList<Integer> myArrayList = new ArrayList<>();

```
2) To put an object in a regular array, you must assign it to a specific location. With ArrayList, you can specify an index using the add(anInt, anObject)
   method, or you can just keep saying add(anObject) and the ArrayList
   will keep growing to make room for the new thing.

```java
myList[1] = 7;
myArrayList.add(3);
```

3) Arrays use array syntax that’s not used anywhere else in Java.
4) ArrayLists are parameterised. They use parameterised types in <> syntax.











