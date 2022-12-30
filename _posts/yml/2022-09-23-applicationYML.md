---
layout: post
title: H2 db connection with application.yml
category: application.yml
tags:
  - application.yml
---

my .yml didnt work and my h2 db table was not created when I 
try running the server

```yaml
spring:
#  profiles:
#    active: local

  h2:
    console:
      enabled: true
  datasource:
    url: jdbc:h2:tcp://localhost/~/codingmates
#    url: jdbc:h2:~/codingMates
    driver-class-name: org.h2.Driver
    username: sa
    password:

  jpa:
    properties:
      hibernate:
        dialect: org.hibernate.dialect.H2Dialect
#        dialect: org.hibernate.dialect.PostgreSQLDialect
        #하이버네이트가 실행하는 모든 SQL문을 콘솔로 출력해 준다.
        show_sql: true
        ddl-auto: create-drop
        #콘솔에 출력되는 JPA 실행 쿼리를 가독성있게 표현한다.
        format_sql: true
        #디버깅이 용이하도록 SQL문 이외에 추가적인 정보를 출력해 준다.
        use_sql_comments: true

  security:
    oauth2:
      client:
        registration:
          facebook:
            client-id: 448679747294984
            client-secret: 279b2d3519d841f59ff33b4a91bbf11c
            auth-endpoint: https://www.facebook.com/dialog/oauth
            token-endpoint: https://graph.facebook.com/oauth/acess_token
            redirect-url: https://127.0.0.1/login/oauth2/code/facebook
            fetching_data_endpoint: https://graph.facebook.com/v15.0/debug_token

          google:
            client-id: 822931905259-5cu7f4rrlrc02st634a33gjku1sovj47.apps.googleusercontent.com
            client-secret: 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
            auth-endpoint: https://accounts.google.com/o/oauth2/auth
            redirect-url: http://localhost:8080/login/oauth2/code/google
            token-endpoint: https://www.googleapis.com/oauth2/v4/token
            fetching_data_endpoint: https://www.googleapis.com/oauth2/v2/userinfo
          github:
            client-id: b07e5cb0ab0e5a2eb7ab
            client-secret: 39564cb9ebb23b5d5c4415096efbfffd8c97cebc
            auth-endpoint: https://github.com/login/oauth/authorize
            token-endpoint: https://github.com/login/oauth/access_token
            fetching_data_endpoint: https://api.github.com/user
    jwt:
      token:
        secret-key: secretKeytestauthorizationjwtmanagetokenjwtmanagetoken
        expire-length: 1800000

---
spring:
  config:
    activate:
      on-profile: "proddb"
  datasource:
    url: jdbc:postgresql://codingmatesdb.c8pa7vtqsrpa.us-west-1.rds.amazonaws.com:5432/coding_mates_db
    driver-class-name: org.postgresql.Driver
    username: postgres
    password: disneyland77

#---
spring:
  config:
    activate:
      on-profile: "localdb"
  h2:
    console:
      enabled: true
  datasource:
    url: jdbc:h2:tcp://localhost/~/codingmates
    driver-class-name: org.h2.Driver
    username: sa
    password:
#
#---
#spring:
#  config:
#    activate:
#      on-profile: "common"
#
#server:
#  port: 8080
#  tomcat:
#    uri-encoding: UTF-8
```

Stressing for like 5 hours, I saw one that fixed it but don't
know how this is different from mine

```yaml
spring:
  profiles:
    group:
      "default": "local"
      "dev": "dev"
      "test": "test"
---
spring:
  profiles:
    active: local

  h2:
    console:
      enabled: true
  datasource:
    url: jdbc:h2:~/codingMates;AUTO_SERVER=true
    driver-class-name: org.h2.Driver
    username: sa
    password:

  jpa:
    hibernate:
      ddl-auto: create-drop
    properties:
      hibernate:
        dialect: org.hibernate.dialect.H2Dialect
        #하이버네이트가 실행하는 모든 SQL문을 콘솔로 출력해 준다.
        show_sql: true
        #콘솔에 출력되는 JPA 실행 쿼리를 가독성있게 표현한다.
        format_sql: true
        #디버깅이 용이하도록 SQL문 이외에 추가적인 정보를 출력해 준다.
        use_sql_comments: true
    defer-datasource-initialization: true
    generate-ddl: true
  sql:
    init:
      mode: always
      schema-locations: classpath:initData.sql
  security:
    oauth2:
      client:
        registration:
          facebook:
            client-id: 626914439027452
            client-secret: ad25fd1b3eb2b01d3a5c7a92610b5697
            auth-endpoint: https://www.facebook.com/dialog/oauth
            token-endpoint: https://graph.facebook.com/oauth/access_token
            redirect-url: https://127.0.0.1/login/oauth2/code/facebook
            fetching_data_endpoint: https://graph.facebook.com/v15.0/debug_token

          google:
            client-id: 822931905259-5cu7f4rrlrc02st634a33gjku1sovj47.apps.googleusercontent.com
            client-secret: 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
            auth-endpoint: https://accounts.google.com/o/oauth2/auth
            redirect-url: http://localhost:8080/login/oauth2/code/google
            token-endpoint: https://www.googleapis.com/oauth2/v4/token
            fetching_data_endpoint: https://www.googleapis.com/oauth2/v2/userinfo
          github:
            client-id: b07e5cb0ab0e5a2eb7ab
            client-secret: 39564cb9ebb23b5d5c4415096efbfffd8c97cebc
            auth-endpoint: https://github.com/login/oauth/authorize
            token-endpoint: https://github.com/login/oauth/access_token
            fetching_data_endpoint: https://api.github.com/user
    jwt:
      token:
        secret-key: secretKeytestauthorizationjwtmanagetokenjwtmanagetoken
        expire-length: 1800000
```
