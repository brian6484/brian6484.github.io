---
layout: post
title: Error in declaring variables in 1 line
category: Java
tags:
  - Java
  - Head First Java
---
## Error
I was solving some Leetcode when I declared variables in 1 line like 
this:
```java
int len=0, min=Integer.MAX_VALUE, from=0;
```

All my logic was right but strangely it didn't work.

Turns out the error is probably due to that min being declared in the
middle

Like this works
```java
int sum=0, from =0, min= Integer.MAX_VALUE;
```
