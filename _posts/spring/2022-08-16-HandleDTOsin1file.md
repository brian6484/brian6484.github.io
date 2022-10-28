---
layout: post
title: How to manage DTOs in Spring Boot well
description: 
category: Spring
tags:
  - Spring

---

## Intro
According to the API spec of project, we can have multiple forms
of DTOs for Request and Response. So we can get multiple DTO files,
which can be visibly messy to manage. 

Is there a way to combine all forms of DTOs into one file for 
better management? Yes, through static nested class!

## Note on nested class
Take a look at [My posted on nested class]() before continuing.

## DTOs via static nested class
[This reference](https://velog.io/@p4rksh/Spring-Boot%EC%97%90%EC%84%9C-%EA%B9%94%EB%81%94%ED%95%98%EA%B2%8C-DTO-%EA%B4%80%EB%A6%AC%ED%95%98%EA%B8%B0)
explained well on how to arrange DTOs.


