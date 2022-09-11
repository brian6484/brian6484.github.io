---
date: 2022-06-23 14:35:23
layout: post
title: Protected
subtitle: JPA
description: 
image: https://res.cloudinary.com/dm7h7e8xj/image/upload/v1559825145/theme16_o0seet.jpg
optimized_image: https://res.cloudinary.com/dm7h7e8xj/image/upload/c_scale,w_380/v1559825145/theme16_o0seet.jpg
category: JPA
tags:
  - Java
  - Spring
  - JPA

  
author: Jeonghwan Lee
---

1. Protected
 * JPA allows Protected as constructor of entity to prevent other ways of creating new object. This can be replaced with Lombok's @NoArgsConstructor

 ```java
@NoArgsConstructor(access = AccessLevel.PROTECTED)
 ```

 * 



