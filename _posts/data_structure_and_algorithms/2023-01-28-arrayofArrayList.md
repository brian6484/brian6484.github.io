---
layout: post
title: What is ArrayList<Integer>[] or StringBuilder[]? What is this square bracket's role?
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
---

## Explanation
It was hard to google it because google search doesnt work well with
symbols. However, I found out that 

```java
ArrayList<Integer>[] G = new ArrayList[n];
StringBuilder[] st= new StringBuilder[numRows];
```

is actually just making an array of ArrayLists or StringBuilders.

The main difference between ArrayList<Integer>[] and ArrayList<Integer> is that the former is an array 
of ArrayList(s), whereas the latter is a single ArrayList. So
when you instantiate the array, you have to assign the initial length,
just like when you instantiate a regular array of int (=new int[3])
