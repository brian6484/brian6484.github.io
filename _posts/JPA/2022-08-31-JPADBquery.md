---
layout: post
title: JPA force DB query when entity is already saved in 1st cache
description: 
category: JPA
tags:
  - JPA
---
  
## Solution
As you know, when we em.persist(entity), we keep the PK as the key
and the entity itself as the value in EntityManger. We can think of
EntityManager as PersistenceContext, although it is different in
some minor ways.

Anyway, this entity is managed by EM and is saved in 1차 cache so that
within the **same database transaction**, if another call is made to 
save or search or update this entity, EM can return it straight from
its 1차 cache and not save a SQL query to be queried to DB once 
transaction.commit() is invoked.

But for logging purpose or to forcefully send the DB query, we have
to get rid of this entity from being managed by EM.

Solution:
```java
em.flush();
em.clear();
```

These 2 commands will do the trick. Remember flush does not flush
out saved entities but it just sends out the query to DB immediately,
even before transaction.commit() can happen. 
