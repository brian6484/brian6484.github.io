---
date: 2022-06-07 14:35:23
layout: post
title: Command Query Separation
description: 
category: General Knowledge
tags:
  - General Knowledge
  - Spring
  - JPA
---

## Introduction of CQS
Reference: https://dundung.tistory.com/183, 
https://hardlearner.tistory.com/383,
https://www.inflearn.com/questions/35961

Command Query Separation (CQS) is all about separating command
and query. The reason to separate them is when there is an issue
regarding unintentional changes made in data, we can just look
at the methods that *cause* change.

### Command
Command, also known as modifiers or mutators in other contexts,
changes state of a system, but do not return a value.

### Query
Query returns a result and do not change the observable state of
the system (free of side effects)

If it does not cause change in internal state of system, it is
free of side effects 

## Example of CQS in JPA
Follow this rule:
> insert는 id만 반환하고 (아무것도 없으면 조회가 안되니), update는 아무것도 반환하지 않고, select (조회)는 내부의 변경이 없는 메서드로 설계하면 좋습니다

Let's look at it one by one.

> insert returns only the id
```java
private EntityManager em;

    @Transactional
    public Long save(Item item){
        em.persist(item);
        Item item = em.find(Item.class, id);
        return item.getId();
  }
```

insert causes change in state of the DB **BUT** at the same time,
returns the value of id. Thus, it is both a command and a query.
It breaks the CQS rule but is needed.

> update does not return anything (query)
```java
private EntityManager em;
    @Transactional
    public  void update(Item item){
        em.persist(item);
  }
```
update causes change in state of the DB but does not return
anything (void). So it is a *command*.

>select(조회) returns result without
chaning state of system (query)
```java
@Transactional
    puiblic Item findOne(Long id){
        Item item = em.find(Item.class,id);
        return item;
    }
```
select(조회) does not change state of system and just returns the
result of sql query so it is a *query*.

## Exception to CQS 
A perfect exception to CQS is stack.pop(). pop()'s command removes
the top value from the stack, thus causing change in stack's
state whilst pop()'s query is getting that popped value. 
Pop() is both a command and query, which is an exception to CQS.

insert id in JPA is also an exception.





