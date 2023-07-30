---
layout: post
title: BooleanExpression in Querydsl and use booleanexpression over booleanbuilder
category: Querydsl 
tags:
  - Querydsl
  
---
## Link
very useful tips for spring boot and especially booleanexpression over booleanbuilder

https://velog.io/@youngerjesus/%EC%9A%B0%EC%95%84%ED%95%9C-%ED%98%95%EC%A0%9C%EB%93%A4%EC%9D%98-Querydsl-%ED%99%9C%EC%9A%A9%EB%B2%95

## BooleanExpression
### Using SprintUtils.hasText() to compare strings
So comparing strings in BooleanExpression is easy we just do
```java
private BooleanExpression reqUrlEq(String reqUrl){
    return StringUtils.hasText(reqUrl) ? statistics.reqUrl.eq(reqUrl) : null;
}
```

Which I just realised hasText is a method in StringUtils class. Why I was 
surprised is because I thought hasText is a method of BooleanExpression.

Anyway, how about comparing LocalDateTime parameter with a search 
condition of LocalDate? For example, I have a createdAt localdatetime 
timestamp for each record created. I want to make a condition to check 
if it is between a search date condition, specifically within today 
date’s LocalDate range (e.g. 2023-04-04). If I just compare with today’s 
LocalDateTime, obviously it wont match cus it has to be exact to the 
microsecond.

So I have been trying to search for a solution and here it is:https://velog.io/@kjy0302014/QueryDsl-Date-%EC%A1%B0%EA%B1%B4-%EC%B2%98%EB%A6%AC

Solution:
We format the incoming LocalDateTime using Expressions.stringTemplate 
and the parameter we pass (“TO_CHAR) depends on your type of db. If you are using H2 like that blog, then you have to use FUNCTION(DATE_FORMAT).

Here it is for Oracle:

```java
String todayDate = String.valueOf(LocalDate.now)
StringExpression formattedDate = Expressions.stringTemplate(“TO_CHAR({0},’yyyy-mm-dd’)”, statistics.createdAt);
Return formattedDate.eq(todayDate);
```

## Example
I needed to build a query that join multiple tables on multiple matching conditions. One of the matching conditions had a field (clientName) that was not present in my main table (Statistics) so I needed to create a separate subquery, to be included in my main query. I implemented BooleanExpressions for the matching where conditions.

```java
public void updateCountIfMatch(String reqUrl, LocalDateTime createdAt, String statusCode, String clientName){
    JPQLQuery<Long> subquery = JPAExpressions.select(statistics.id)
//  blabla
}
```


I thought in the JPQL subquery, I need to select client.clientName, which was the field that I want to match and it wasnt in my stats table but actually, statistics.id needs to be selected to be the primary identifier for the main query.

