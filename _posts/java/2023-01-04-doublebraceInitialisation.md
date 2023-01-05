---
layout: post
title: Double brace initialisation in Java
category: Java
tags:
  - Java
  - Head First Java
---
## Tada
```java
Map<Integer, Integer> map = new HashMap<>();
// corner case: if the very first subarray with first two numbers in array could form the result, we need to 
// put mod value 0 and index -1 to make it as a true case
map.put(0, -1);
```
is same as:
```java
Map<Integer, Integer> map = new HashMap<>(){{put(0,-1);}};;
```

How?

It is actually called [double brace initalisation](https://stackoverflow.com/questions/1958636/what-is-double-brace-initialization-in-java)
which is discussed in https://leetcode.com/problems/continuous-subarray-sum/solutions/99499/java-o-n-time-o-k-space/?orderBy=most_votes
comments
