---
layout: post
title: Problem of overflow with lambda
category: Java
tags:
  - Java
  - Head First Java
---
## Issue
I was using Lambda to sort order of elements going into my priority
queue.
```java
PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[2] - b[2]);
```

While it will work perfectly fine in most cases, it can cause
overflow issue.

It should return positive number if a[2] > b[2], but if a[2] - b[2] > Integer.MAX_VALUE, then might overflow exist. 

For example: a[2] = Integer.MAX_VALUE, b[2] = -2, then a[2] - b[2] < 0

## Solution
Well consider this overflow issue and implemnt the logic to prevent
it
```java
PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[2] < b[2] ? -1 : a[2] == b[2] ? 0 : 1);
```
 
Or more simply, Integer.compareTo will solve this problem.
```java
(a, b) -> (Integer.compare(a[0], b[0]))
```
