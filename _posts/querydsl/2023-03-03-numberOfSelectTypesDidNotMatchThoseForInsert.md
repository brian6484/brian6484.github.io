---
layout: post
title: How to set up Querydsl in your Spring Boot gradle project
category: Querydsl 
tags:
  - Querydsl
  - Database

  
---
## Issue
So i was trying to insert into columns of my stats table the data taken 
from serviceLog when I saw this error. I first checked if there is an 
extra field that I was trying to insert. But the field number was the 
same at 14.

Then I just deleted all fields except one field just to test if just 
a single field can be inserted without problem. Another error occurred.

> querysyntaxeception unexpected end of subtree [insert into stats(brokertxid) select (select serviceLog.brokerTxId from serviceLog)]

Turns out my syntax of querydsl query was wrong. I was using a subquery inside the select() as I didnt want my query to be too long.

Before:
```java
JPQLQuery<Tuple> subQuery = JPAExpressions.select(serviceLog.brokerTxId).from(serviceLog)

queryFactory.insert(statistics)
.columns(statistics.brokerTxId)
.select(JPAExpressions.select(subQuery))
.execute()
```

As you can see I was calling JPAExpressions twice.

After:
```java
queryFactory.insert(statistics)
.columns(statistics.brokerTxId)
.select(subQuery)
.execute()
```

It worked now!

BTW I checked the column constraints as ChatGPT suggested that 
the difference in TYPE of column may also cause this error. 
(e.g. varchar2(50) instead of number(10,0)). I checked and yep one 
of the fields was max 40 instead of 4000. The error occurred when I was
inserting that specific field.
