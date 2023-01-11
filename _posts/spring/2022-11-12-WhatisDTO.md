---
layout: post
title: What is DTO and its difference between VO?
category: Spring
tags:
  - Spring
---

## Diff between DTO and VO
VO has the same concept as DTO, but has read only properties. VO is an object that contains specific business values, and DTO is an object that comes and goes for the **purpose of communication between layers**.

## Why use DTO?
1) Circular referencing can be prevented - if you use
bidirectional references
2) Can encapsulate internal implementation of an entity
3) Can separate roles between DB and View layer
