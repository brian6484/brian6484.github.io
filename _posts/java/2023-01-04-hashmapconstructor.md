---
layout: post
title: How to use HashMap constructor
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
