---
layout: post
title: Java Stream Matching its values
subtitle: Java 
description: Java
category: Java
tags:
  - Java
  - Head First Java
---
  
* There are 3 ways to validate elements of a sequence according to some predicate. Put it more simply,
check elements for a specific condition.

1) allMatch() checks if ALL elements meet the predicate 
2) anyMatch() checks if there is at least 1 element that meets predicate
3) noneMatch() checks if none meets the predicate

```java
public static void main(String[] args){
        int[] intArr = {2, 4, 6};

        boolean result = Arrays.stream(intArr)
                .allMatch(a -> a%2 == 0);
        System.out.println("2의 배수? " + result);

        result = Arrays.stream(intArr)
                .anyMatch(a -> a%3 == 0);
        System.out.println("3의 배수가 하나라도 있나? " + result);

        result = Arrays.stream(intArr)
                .noneMatch(a -> a%3 == 0);
        System.out.println("3의 배수가 없나? " + result);
}

2의 배수? true
3의 배수가 하나라도 있나? true
3의 배수가 없나? false
```


 
