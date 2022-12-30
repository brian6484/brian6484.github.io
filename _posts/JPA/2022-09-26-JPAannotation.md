---
date: 2022-09-26 14:35:23
layout: post
title: Basic JPA annotations you should know (e.g. PersistenceContext, Transactional, etc)
subtitle: Spring 
description: Spring 
category: Spring
tags:
  - Spring
  
---


## @PersistenceContext
to DI EntityManager

## @PersistenceUnit
to DI EntityManagerFactory

## @Transactional
can add "readOnly=true" to apply to all methods in that class
that are only for read usages (NOT write usages)

If there is write method, need to delcare exception via
adding @Transactional to that method

I explained more on my previous post on @Transactional

## @Autowired
Should be using constructor DI over @Autowired DI whenever you
can

If there is 1 constructor, can omit @Autowired
