---
layout: post
title: Useful Java data conversion tricks
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
---
## Character.isDigit()
boolean isDigit(char ch) checks if this character is a digit

## char c >= '0'

## s.charAt(i)-'0'
When converting character (e.g. ‘3’) to integer to use as index in array, have to subtract ASCII value of ‘0’.

## int s = Character.getNumericValue(secret.charAt(i));
This is same as doing s.charAt(i)-'0', getting the int value of char.

## string to set<Character>
```java
Set<Character> set1= "qwertyuiop".chars().mapToObj(c-> (char)c).collect(Collectors.toSet());
```

## converting ArrayList to Array for int[] solution
```java
List<String> result = new ArrayList<>();
result.toArray(new String[result.size()]);
```

## convert array to ArrayList and add in constructor
```java
Set<Character> set = new HashSet<>(Arrays.asList('a','e','i','o','u','A','E','I','O','U'));
```
