---
layout: post
title: Spring Security's default Login page feature
category: Spring 
tags:
  - Spring
  - Spring Security
  
---
## Initial confusion
when using spring security, whenever I start the Java application it 
kept prompting me to a /login page that prompted me to enter a username 
and password. But I have never made this html file before so I was 
confused. 

## Spring Security comes with default login feature
Actually, this is the default page that you HAVE to authenticate 
yourself before you can access your HTML files. Username is user and 
password is the long password given in the console. And worse thing is 
you have to authenticate EVERYTIME you restart your application. This is 
cumbersome so add 
@SpringBootApplication(exclude = SecurityAutoConfiguration.class) 
annotation onto your Application class. This removes this authentication 
page.
