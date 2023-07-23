---
date: 2022-03-05 14:35:23
layout: post
title: JPA FetchType
description: 
category: JPA
tags:
  - JPA
---
When JPA fetches data, there are 2 options of FetchType - EAGER and
LAZY.

## Intro of JPA FetchType
The default for JPA FetchType is that 
* @xxToOne - EAGER
* @xxToMany - LAZY

FetchType is the default value of how to bring in the
connected entities in 연관관계 when JPA searches for one specific
entity.

* Through ORM, we don't have to create the queries ourselves because
JPA automatically creates them for us using JPQL.
* JPA looks at the entities and fields to create queries.
* Thus, if the entity is mapped to other entities in 연관관계, JPA looks
up at them too. We can tell JPA how to look them up through FetchType.

## FetchType.EAGER
```java
@Entity
public class Member {

    @Id @GeneratedValue
    private Long id;
    private String username;

    //default is Eager for xxToOne so no need to declare like this
    @ManyToOne(fetch = FetchType.EAGER) //Team을 조회할 때 즉시로딩을 사용하곘다!
    @JoinColumn(name = "team_id")
    Team team;
}

@Entity
public class Team {

    @Id @GeneratedValue
    private Long id;
    private String teamname;
}
```

Let's do 1 search query of member with JPQL
```java
Member findMember = em.createQuery("select m from Member m", Member.class).getSingleResult();
```

```sql
//멤버를 조회하는 쿼리
select
    member0_.id as id1_0_,
    member0_.team_id as team_id3_0_,
    member0_.username as username2_0_ 
from
    Member member0_

//팀을 조회하는 쿼리
select
    team0_.id as id1_3_0_,
    team0_.name as name2_3_0_ 
from
    Team team0_ 
where
    team0_.id=?
```

With EAGER, when it searches MEMBER, it also does a query to bring
TEAM. No proxy but the actual entity.

## EnumType.LAZY

Let's change to LAZY type now.

```java
@ManyToOne(fetch = FetchType.LAZY)
```

When we do the same JPQL query, we get:
```sql
//Team을 조회하는 쿼리가 나가지 않음!
select
    member0_.id as id1_0_,
    member0_.team_id as team_id3_0_,
    member0_.username as username2_0_ 
from
    Member member0_
```
The connected entity (team) is not queried.

This is done via querying team via proxy, not the actual entity
object. Don't belive me? Let's try this code

```java
Member m = em.find(Member.class, member1.getId());
System.out.println(m.getTeam().getClass());
```

The output will be a proxy. So the only true entity (not proxy) that is queried is
member.

One important side-note is that when we do something like
m.getTeam().getName() where we query some fields of Team, only then
will the queries for Team entity be executed. This is because
DB has been 초기화ed.

Another example?

When FetchType is Lazy and we have a collection like
```java
Member member = em.find(Member.class, “member1”)
List<Order> orders = member.getOrders()
Sout ordergs.getClass().getName()
```

Hibernate keeps track of the original collection, whilst converting it 
to Hibernate’s internal collection called **collection wrapper**. In 
this case, it will print 

`org.hibernate.collection.internal.PersistentBag`

For entities in lazy setting, Hibernate uses proxy but for collections 
like orders, Hibernate uses collection wrapper. This collection wrapper 
does the role of a proxy so let’s just call it proxy.


## N+1 issue
With EAGER, when we query for member, query for 연관된 객체 team is
also generated. But with LAZY, the mapped entity (team) is not
needed so only query for member is generated.

If member 연관된 team object is not 1 but N number of objects,
wtih EAGER, when we want to search just 1 member, query for 
team adds up to N queries (N+1 problem)

## When LAZY is not better than eager
Most of the time, LAZY should be user. But lazy is not always “better” 
than eager. Briefly explaining, when we do

```java
em.find(Member.class, “member1”)
```

We get the actual member instance but we dont get the actual team object 
like eager. We get a team **proxy** instead when we do

```java
Team team = member.getTeam()
```

Until we call one of Team’s methods like team.getName(), only then we 
will get the actual entity instead of proxy.

Ok coming back, eager is actually more efficient for entities that are 
connected and used commonly than lazy. So if member and team are used 
tgt a lot, **set it as EAGER, not LAZY**. This is because EAGER will use 
*SQL outer join* to search all member and team entities in 1 go, rather 
than separate SQL queries that Lazy will do.

The recommended way is first to put ALL 연관관계 as lazy. Then when code 
is almost complete, look at actual connect and how much entities are 
commonly used together then set those as eager. Also, for 1 entity can 
use Eager but for a collection, use Lazy cuz loading a collection is 
expensive and can load a lot of data.

## One-line summary
Use LAZY !! But don't be LAZY!
