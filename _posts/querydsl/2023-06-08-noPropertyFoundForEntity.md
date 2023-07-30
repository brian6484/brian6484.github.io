---
layout: post
title: error no property "some_method_name" not found for type "entity"
category: Querydsl 
tags:
  - Querydsl
  
---
## Issue
Actually the solution is easy cuz I have been ignoring the method that I used QueryDsl on is not being recognised by other java class files, as shown in method name highlighted in grey colour.

The solution:
https://velog.io/@3210439/querydsl-No-property-found-for-type

When you use querydsl, the repo name has to follow a certain convention

`
holaRepoCustom <- interface, 
holaRepoImpl <- implementation
`

These Custom and Impl keywords have to be at the end of the repo name

So I renamed all the usages and file names and it worked!
