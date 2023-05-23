---
layout: post
title: When should your repoImpl extend Querydsl querydslrepositorysupport?
category: Querydsl 
tags:
  - Querydsl

  
---
## Issue
Your repoimpl should extend querydslrepositorysupport when you need 
some **advanced querydsl functionalities** - *BooleanExpression and Predicate 
class* to make your **custom** queries. For example if you need filtered 
search queries on certain conditions passed by your conditiondto like

```java
select(logs.*, clientInfo.clientId, client.clientName)
.from(logs)
.leftjoin(clientInfo)
.on(clientInfo.code.eq(logs.code)) //match on common fields that both tables share
.on(clientInfo.name.eq(logs.name))
.leftjoin(client)
.on(client.id.eq(clientInfo.clientId))
  
  // boolean expressions used here
.where(nameEq(conditionDto.getName()),
codeEq(conditionDto.getCode()))
.orderBy(logs.createdAt.desc())
.offset(pageable.getOffset())
.limit(pageable.getPageSize())
.fetch();

JpaQuery<Long> countQuery = queryFactory
.select(logs.count())
.from(logs)
//blabla all the way till where conditionDto

```

Now here we created a custom method to check in where condition - 
nameEq and codeEq

```java
Private BooleanExpression codeEq(String name){
Return hasText(name) ? client.name.contains(name) : null
```

