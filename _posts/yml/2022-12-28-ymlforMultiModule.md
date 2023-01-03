---
layout: post
title: application.yml for Multi-Module (feat. AWS RDS settings)
description: 
category: application.yml
tags:
  - application.yml

---

## Intro
There will be multiple yml files for each of your modules.
For example, in module-member, I have 3 yml (test,dev,local)
and so in each module I have 3 yml files.

However, let's go back a step. Before we did multi-module,
there was 1 single yml file for our application. This is located
in the very bottom src folder where our mainApplication.java file
is. 

THAT is where we add our DB details.

For example, for my dev environment to be deployed to AWS,
I need to add my AWS RDS details to my yml file. Do this 
not in the module yml file but in this final yml file.

BTW, AWS RDS details are like this:
```yaml
spring:
  datasource:
    url: jdbc:mysql://{엔드포인트}:5432/{데이터베이스이름}?useSSL=true&characterEncoding=UTF-8
    username: {사용자명 (default: admin)}
    password: {비밀번호}
    driver-class-name: org.postgresql.Driver
```

The url is the full url of your DB, not just the endpoint.
You can get these details via:
1) clicking Database on the most-right column 
2) (4th button) Data Source Properties

