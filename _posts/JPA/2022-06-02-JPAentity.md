---
layout: post
title: What is entity and its precautions when designing in JPA?
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

## How are entities mapped?
```java
@JoinColumn(name = “name_of_FK_joining_2_tables”)
//Name is “team_id” or name of FK
```

If you omit this attribute, JPA finds FK via
Field name (team) + _ + table column name reference like

`(TEAM_ID) = team_TEAM_ID`

## Precautions
### Never use setters indiscriminately
When creating entities, indiscriminate use of setters can change the value of an object (Entity), so object consistency cannot be guaranteed.
To elaborate, when entity is managed by PersistenceContext and
its value is changed, its updated value is updated into DB.
But if setter is open to be used, it opens up random accidental
changes of its value, making it hard for 유지보수.
This applies not only to entity, but DTO as well.

### All 연관관계 in LAZY
I explained this in my [fetchType post](https://brian6484.github.io/jpa/2022/03/05/JPAFetchType.html)

### Reset collections at field level immediately
Tbc




