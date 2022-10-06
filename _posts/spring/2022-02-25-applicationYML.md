---
date: 2022-02-25 14:35:23
layout: post
title: Tips on application.yml
subtitle: Spring
description: 
category: Spring
tags:
  - Spring
---

## Logging
1) trace allows us to see what parameter values are passed. Without
this, insert into member (username, id) values (?, ?) so here we
don't know what values are passed. With this, in the log we can 
see binding parameter [1] etc

```yaml
logging:
  level:
    org.hibernate.type: trace
```

However, an alternative to actually see the values being substituted
inside (? , ?) is to use an external library

Link: https://github.com/gavlyukovskiy/spring-boot-data-source-decorator

To use this, add in your build.gradle:
```yaml
implementation 'com.github.gavlyukovskiy:p6spy-spring-boot-starter:1.5.6'
```

But in production server, must do a performance test on this





