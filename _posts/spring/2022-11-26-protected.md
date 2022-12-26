---
layout: post
title: Protected annotation
category: Spring
tags:
  - Spring
  
---
## Protected

JPA allows Protected as constructor of entity to prevent other ways of creating new object. 
This can be replaced with Lombok's @NoArgsConstructor.

 ```java
@NoArgsConstructor(access = AccessLevel.PROTECTED)
 ```




