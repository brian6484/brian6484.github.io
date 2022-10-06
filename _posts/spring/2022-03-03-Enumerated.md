---
date: 2022-03-03 14:35:23
layout: post
title: Enumerated annotation and its EnumType types
description: 
category: Spring
tags:
  - Spring

---

## Enum
reference: https://ttl-blog.tistory.com/115

When we use @Enumerated annotation to map Java's Enum type, we
have 2 EnumType types to choose from

```java
enum Gender{
    MALE,FEMALE
}
```

## EnumType.ORDINAL
This saves the order of enum. So MALE = 0, FEMLAE =1 values are
saved in the DB.

* Advantage: Saved data size is small since it is just integers.
* Disadvantage: We can't change the order of enum that is already saved
in the DB. So if we add a new Enum due to new business logic, like
{MALE, NONE, FEMALE} numbers in db get messed up.

## EnumType.STRING
This saves the string of enum as it is. 

* Advantage: When new enum is added or when the already-saved enum's
order is changed, no problem!
* Disadvantage: more data saved but worth it

## One-liner summary
Use EnumType.STRING!
