---
date: 2022-09-21 14:35:23
layout: post
title: Error: BeanCreationException at AbstractAutowireCapableBeanFactory
subtitle: Spring 
description: Spring 
category: Spring
tags:
  - Spring
  
---

When there were multiple .yml and .properties, .properties-local files, I got this error:

Caused by: org.springframework.beans.factory.BeanCreationException at AbstractAutowireCapableBeanFactory.java

I deleted all the .properties files until there was only 1 .yml file and the remaining errors were
resolving the paths of values in conflicted class by replacing them with yml paths. For example, there were missing values (@Value)
in my yml file that were present in properties file, like in AuthService.class,
tokenEndpoint and fetchingDataEndpoint values were missing in my yml file. So I added them
in my yml file.

But if you don't add the values, values cannot be found and injected via @Value, so
beans will not be created.

One tricky thing was getting the path of jwt token properly. The path starts from
.spring, like any other values but I missed it. Also, if you look closely, path does
not incldue .oauth2 so please look at yml path carefully.

This is example of how paths should be:
```java
    public TokenProvider(
            @Value("${spring.security.jwt.token.secret-key}") String secret,
            @Value("${spring.security.jwt.token.expire-length}") long tokenValidityInSeconds) {
        this.secret = secret;
        this.tokenValidityInMilliseconds = tokenValidityInSeconds * 1000;
    }
```



