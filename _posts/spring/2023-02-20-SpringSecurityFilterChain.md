---
layout: post
title: Careful with Spring Security's SecurityFilterChain (front slash for url!)
category: Spring 
tags:
  - Spring
  - Spring Security
  
---
## ALWAYS put front slash at start of URL
For Spring security’s SecurityFilterChain, PLEASE PLEASE PLEASE be careful
with the url.

The url **has** to start with front slash / like “/users/listViewAdmin”. I 
did not place front slash in front of my url like 
```java
.antMatchers(“users/listViewAdmin”).permitAll()
//should be /users/listViewAdimin
```
so I was confused why this url was making me authenticate myself when 
I explicitly mentioned it to be permitted without authentication. Always 
remember front slash. It is not the String html file name you return in 
your Controller. It is a URL so always remember front slash.


