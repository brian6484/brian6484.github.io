---
date: 2022-06-01 14:35:23
layout: post
title: Controller VS RestController
subtitle: Java
description: 
image: https://res.cloudinary.com/dm7h7e8xj/image/upload/v1559825145/theme16_o0seet.jpg
optimized_image: https://res.cloudinary.com/dm7h7e8xj/image/upload/c_scale,w_380/v1559825145/theme16_o0seet.jpg
category: Java
tags:
  - Java
  - Spring

  
author: Jeonghwan Lee
---

1. @Controller VS @RestController

* If return value of @Controller is String, it is rendered as *view* but for @RestController, return value is inserted into HTTP message body. 

2. @RequestMapping

* If no HTTP method is allocated in @RequestMapping, all HTTP methods are allowed.

* If prohibited HTTP method is called, 405 (Method not allowed) is returned.

* 







