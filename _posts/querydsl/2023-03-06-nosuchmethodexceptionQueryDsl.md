---
layout: post
title: Querydsl noSuchMethodException
category: Querydsl 
tags:
  - Querydsl

  
---
## Issue
> querydsl expressionexception iarstatisticswithpartnerdto with root 
>cause java.lang.nosuchmethodexception

So I was encountering that exception error when I was using querydsl in
my repo. I have placed @Data annotation on my DTO, which I have been 
doing for my toy project as well and found no problem. But upon 
googling, I found that my understanding of this annotation is misplaced.

@Data annotation comprises of 5 annotations in Lombok - getter, setter, 
requiredargsconstructor, tostring and equalsandhashcode.

When using projection with querydsl, it is a **MUST** to include a 
constructor. RequiredArgsConstructor is not making a constructor in 
this case cuz all of my fields of my DTO are **not final**.

So as a solution, just create a basic constructor that takes no arguments like 
@NoArgsConstructor. Or you can put both noargs and allarags.
