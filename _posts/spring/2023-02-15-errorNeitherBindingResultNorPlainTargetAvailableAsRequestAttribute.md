---
layout: post
title: Error Neither BindingResult nor plain target object for bean name '...' available as request attribute
category: Spring 
tags:
  - Spring
  
---
## Solution
1. Controller.java 에서 @ModelAttribute 있는지 확인.

```java
@RequestMapping(value="/register")
public String join(@ModelAttribute("memberVO") @Valid MemberVO memberVO, BindingResult bindingResult){
```

BTW no need to initialise name for @ModelAttribute("memberVO") because it
automatically takes the parameter as its name (key). But if you want another
name for your modelAttribute, then yep.

2. Controller's @ModelAttribute("memberVO") @Valid MemberVO memberVO 와
jsp or thymeleaf의 <form:form action="/register/step3" commandName="memberVO"> 이
같아야함.

Explained well here https://velog.io/@minnseong/Neither-BindingResult-nor-plain-target-object-for-bean-name-questionForm-available-as-request-attribute-%EC%98%88%EC%99%B8

But the solution in that above link is not ideal so look at that 2 solutions on top


