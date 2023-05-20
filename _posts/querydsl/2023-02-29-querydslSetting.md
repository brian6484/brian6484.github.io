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

## yml file
```yaml
plugins {
    id 'org.springframework.boot' version '2.6.3'
    id 'io.spring.dependency-management' version '1.0.11.RELEASE'
    // 2. querydsl plugins 추가
    id "com.ewerk.gradle.plugins.querydsl" version "1.0.10"
    id 'java'
}

dependencies {
    // 3. querydsl dependencies 추가
    implementation "com.querydsl:querydsl-jpa:${queryDslVersion}"
    implementation "com.querydsl:querydsl-apt:${queryDslVersion}"
    //...
}

test {
    useJUnitPlatform()
}

/*
 * queryDSL 설정 추가
 */
// querydsl에서 사용할 경로 설정
def querydslDir = "$buildDir/generated/querydsl"
// JPA 사용 여부와 사용할 경로를 설정
querydsl {
    jpa = true
    querydslSourcesDir = querydslDir
}
// build 시 사용할 sourceSet 추가
sourceSets {
    main.java.srcDir querydslDir
}
// querydsl 컴파일시 사용할 옵션 설정
compileQuerydsl{
    options.annotationProcessorPath = configurations.querydsl
}
// querydsl 이 compileClassPath 를 상속하도록 설정
configurations {
    compileOnly {
        extendsFrom annotationProcessor
    }
    querydsl.extendsFrom compileClasspath
}
```

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
