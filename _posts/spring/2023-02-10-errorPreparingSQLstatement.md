---
layout: post
title: Error - preparing SQL statement
category: Spring
tags:
  - Spring
  
---
## Error
At the repository level, I usually place @DataJpaTest instead @SpringBootTest
as it is lighter than running everything with @SpringBootTest. But I got
this error Error - preparing SQL statement. I was using H2 DB.

## Solution
Change @DataJpaTest to @SpringBootTest as recommended here.

https://velog.io/@jwkim/spring-boot-datajpatest-error

**This normally happens with H2 DB** as I have not seen this error in other DBs.

The reasoning behind this is that @DataJpaTest's @AutoConfigureTestDatabase
does not connect to the H2 DB in config. Instead, it connects to a 
temporary H2 DB that is temporarily set-up via EmbeddedDatabaseConnection.

