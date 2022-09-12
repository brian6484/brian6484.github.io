---
date: 2022-06-07 14:35:23
layout: post
title: PathVariable
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

 * 2 most common ways that client sends parameters thorugh URL is: 1) http://ip?index=1&page=2 2) http://ip/index/1 . 1 is normally used in posts or pages whilst 2 is used in REST API. 1) is used by @RequestParam while 2) is used by @PathVariable


1. @PathVariable

  * **Commonly used with REST API** so type 2

  * It takes care of incoming URL by binding incoming url's parameter into local variable.

```java
@GetMapping("/mapping/{userid}")
public String hello(@PathVarible("userId") String data){
  return "ok";
}
```

2. @RequestParam
* takes care of type 1 of URL

3. Simultaneous usage of @PathVariable and @RequestParam








