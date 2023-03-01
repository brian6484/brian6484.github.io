---
layout: post
title: Java regex
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
---
## W
It matches any non-word character like * or # or whatever. It can be
used with other methods like
```java
//paragraph = "Bob hit a ball, the hit BALL flew far after it was hit."
String[] words = p.toLowerCase().split("\\W+");
```

## s
It matches any whitespace character. We can use with .split() to split
string via whitespaces like:
```java
String str = "Hello, World!";
String[] words = str.split("\\s+");
//Hello,
//World!
```

## .replaceAll()
It replaces the pattern passed as first parameter with the second 
pattern parameter.
```java
//set * at index i
sb.setCharAt(i,'*');
//replaces all * with non-white space
sb.toString().replaceAll("\\*","");
```
