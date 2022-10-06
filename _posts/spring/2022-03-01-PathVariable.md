---
date: 2022-03-01 14:35:23
layout: post
title: PathVariable annotation
description: 
category: Spring
tags:
  - Spring

---

 * 2 most common ways that client sends parameters thorugh URL is: 1) http://ip?index=1&page=2 2) http://ip/index/1 . 1 is normally used in posts or pages whilst 2 is used in REST API. 1) is used by @RequestParam while 2) is used by @PathVariable

## @PathVariable

  * **Commonly used with REST API** so type 2

  * It takes care of incoming URL by binding incoming url's parameter into local variable.

```java
@GetMapping("/mapping/{userid}")
public String hello(@PathVarible("userId") String data){
  return "ok";
}
```

## @RequestParam
* takes care of type 1 of URL

## Simultaneous usage of @PathVariable and @RequestParam








