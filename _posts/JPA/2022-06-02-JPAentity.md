---
layout: post
title: What is entity in JPA?
subtitle: JPA
description: 
category: JPA
tags:
  - JPA
---

## Entity
The Entity class is a class that is mapped 1:1 with tables 
in the actual database. It should only have columns that
exist in the DB as attributes.

## Never use setters indiscriminately
When creating entities, indiscriminate use of setters can change the value of an object (Entity), so object consistency cannot be guaranteed.
This applies not only to entity, but DTO as well.


