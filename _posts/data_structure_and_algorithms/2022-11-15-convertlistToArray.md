---
layout: post
title: How to convert ArrayList to array?
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
---
## Example
Suppose we have a ArrayList of type integer array like this:
```java
List<int[]> list = new ArrayList<>();
```

we use .toArray method to convert List instance to array
```java
list.toArray(new int[list.size()][]);
```

If list.size() is 4, it creates an array of size 4.
