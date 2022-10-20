---
layout: post
title: Controller VS RestController
category: Spring
tags:
  - Spring
  
---
## @Controller VS @RestController

If return value of @Controller is String, it is rendered as *view* but for @RestController, return value is inserted into HTTP message body. 

## @RequestMapping

If no HTTP method is allocated in @RequestMapping, all HTTP methods are allowed.

If prohibited HTTP method is called, 405 (Method not allowed) is returned.









