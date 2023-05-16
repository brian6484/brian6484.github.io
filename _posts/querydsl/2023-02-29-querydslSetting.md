---
layout: post
title: How to set up Querydsl in your Spring Boot gradle project
category: Querydsl 
tags:
  - Querydsl

  
---
## Set-up
Querydsl setting and getting all columns of User entity except password 
column

Follow this guide https://velog.io/@peppermint100/JPA%EC%99%80-QueryDSL
And this https://data-make.tistory.com/728

1) Make QuerydslConfig class in config directory to DI JPAQueryFactory
2) Make UserDetailResponseDto cuz you never want to directly return a entity
3) Mark the constructor of Dto with this @QueryProjection annotation
4) Create UserRepositoryCustom interface and make a method
5) Create UserRepositoryImpl that implements that interface and the query is as such:

```java
public List<UserDetailResponseDto> q_listViewExceptPassword(){
    return query.select(new QUserDetailResponseDto(user.id, user.userId, 
  user.email, user.userStatus))
                .from(user)
                .fetch();
```


Read this for Querydsl https://velog.io/@peppermint100/QueryDSL-%EA%B8%B0%EB%B3%B8-%EB%AC%B8%EB%B2%95 
and especially difference between List of *tuple* and List of *dto* 
implementation 
