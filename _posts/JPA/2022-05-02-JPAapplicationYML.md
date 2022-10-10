---
date: 2022-05-02 14:35:23
layout: post
title: JPA application.yml Hibernate settings explained
subtitle: JPA
description: 
category: JPA
tags:
  - JPA
---

## JPA Hibernate settings
Let me arrange some common settings with explanation.

## ddl-auto 
```yaml
jpa:
  hibernate:
    ddl-auto: none / create
```

Setting to none persists data in the db so can keep reusing it. Setting to create 
refreshes db each time so no data is saved. None is useful when you feel lazy inputting
data over and over while testing.




