---
layout: post
title: Classappend and No-operation (_) in Thymeleaf
description: 
category: Thymeleaf
tags:
  - Thymeleaf

---

## Purpose of th:classappend and no-operation (_)
Referring back to [my previous example of checking validity of input fields by user](https://brian6484.github.io/spring/2022/11/01/SafeNavigationOperator.html)

Observe this html with no-operation (_)
```html
<input type="text" th:classappend=
  "${errors?.containsKey('itemName')} ? 'field-error' : _"
 class="form-control">
```

Through classappend, if there is an error with a particular field,
it is added to the "field-error" class info and **makes the
form red** for emphasis.

No-operation, as marked by the underscore (_), does not do anything.
So if there is no error, it does nothing.

