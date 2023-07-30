---
layout: post
title: ExpressionUtils.sum() not allowed in querydsl
category: Querydsl 
tags:
  - Querydsl
  
---
## Issue
ok so in querydsl, there isnt a ExpressionUtils.sum() like
```java
queryFactory
    .select(ExpressionUtils
      .sum(Expressions
          .when(log.statusCode.isNull())
          .then(1)
          .otherwise(0))
          .add(stats.relayFailCount)
        .as(relayFailCount))
    .from(log)
    .fetch();

```

Sequence number is not allowed here. This error was seen so many times
I think it will show up in my dreams. I tore down my code to the 
foundations and this + changing database schema from NUMBER to INTEGER 
solved the error:

```java
JPAExpressions.select(
New CaseBuilder()
.when(log.statusCode.isNull())
.then(1)
.otherwise(0)
)
.from(log)
```

