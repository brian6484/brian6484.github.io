---
layout: post
title: Limitations of subquery in Querydsl
category: Querydsl 
tags:
  - Querydsl
  
---
## Issue
insert into select can ~ be done via querydsl with JPAExpressions
https://www.inflearn.com/questions/34751/%EC%84%9C%EB%B8%8C%EC%BF%BC%EB%A6%AC-insert%EC%97%90-%EB%8C%80%ED%95%9C-%EC%B2%98%EB%A6%AC

BUT insert into with **group by** functionality + select CANNOT be done via 
querydsl. So as recommended in link, try with JPQL and if cannot, no 
choice but to write a sql query and execute via JDBC template

Both approaches were using scheduling cron.

## With native sql (without querydsl)
```java
//Pure native sql:
String sql =
    "INSERT INTO STATS( " +
    "NAME_HOLA , " +
    "CAN_COLA ” +
    ") " +
    "SELECT " +
    "LOG.NAME_HOLA ,” +
    "TRUNC (LOG.CREATED_AT) , "+
    "SYSDATE , " +
    "SUM (CASE WHEN LOG.CODE LIKE ‘CCIR%’ THEN 1 ELSE 0 END) AS BITCH_COUNT " +
    "FROM " +
    "BITCH_LOG LOG " +
    
    //for getting data for yesterday
    "WHERE " +
    "TRUNC(LOG.CREATED_AT) = TRUNC(SYSDATE) -1 " +
    "GROUP BY " +
    //group by ALL non-aggregate fields
    "LOG.NAME, ” +
    "TRUNC(LOG.CREATED_AT)” ;
    
    jdbcTemplate.execute(sql);
```

** ALWAYS end the pure sql query with semicolon or it will result in error**

## with querydsl
What I tried with querydsl:
All worked EXCEPT the subquery included groupBy expression, which I needed.
The query is in the link above where I posted the question

Integer successCount = 0
```java
JPQLQuery<Tuple> subQuery = JPAExpressions.select(
    log.name,
    log.content,
    new CaseBuilder()
    .when(log.statusCode.eq("0")
    .then(sucessCount+1)
    .otherwise(successCount),
    client.id
)
.from(log)
.leftJoin(client)
.on(client.name.eq(log.name))
//이 group by가 문제
.groupBy(log.name, log.content, client.id);

queryFactory.insert(stats)
.columns(
    stats.name,
    stats.content,
    stats.successCount,
    stats.clientId
)
.select(subQuery)
.execute();
```


