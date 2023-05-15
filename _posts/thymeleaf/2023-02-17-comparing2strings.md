---
layout: post
title: Comparing 2 strings in thymeleaf
description: 
category: Thymeleaf
tags:
  - Thymeleaf

---

## String comparison in Java
As you know in Java, we cannot compare 2 strings with the == equal operator.
The == operator is used to compare **object references**, not the primitive
values. So effectively it checks if they have the same memory address, which
they don't.

## String comparison in Thymeleaf
If you want to compare 2 strings in thymeleaf with th:if

Wrong code:
```html
th:if=”${userAdapter.user.userStatus}==’ADMIN’”
```


Instead, you have to use Thymeleaf’s **strings.equals()** method like this

Correct code:
```html
th:if=”${#strings.equals(userAdapter.user.userStatus, ‘ADMIN’)}”
```

If you want to do the opposite of !equals, add ! infront of # like
${!#string.equals(a,b)}




