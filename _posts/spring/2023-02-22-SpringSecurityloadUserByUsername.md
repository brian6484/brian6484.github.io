---
layout: post
title: NullPointer with Spring Security's loadUserByUsername
category: Spring 
tags:
  - Spring
  - Spring Security
  
---
## Problem
Spring Security login error of invalid username and password and a 
NullPointerException that loadUserByUsername was getting null.

## Solution
So the issue is that my User entity, I am using "userId" as a field, not 
"username". But Spring security login requires the explicit naming of 
“username”, not “userId”. I tried changing the userId variable name in 
“loginForm.html” to username and the functions like public UserDetails 
loadUserByUsername to take in “username” parameter. But it still didnt work.


Solution: in my 회원가입 register.html, my div for userId was as such:

```html
<div>
 <label for=”userId”> User Id:
 <input type =”text” id=”userId” th:field=*{userId}” >
 <div class =”field-error” th:errors=”*{userId}”><div>
</div>
```

But when I changed the id tag from “userId” to “username”, it finally 
worked. Like this:

```html
<div>
 <label for=”username”> User Id:
 <input type =”text” id=”username” th:field=*{userId}” >
 <div class =”field-error” th:errors=”*{userId}”><div>
</div>

```

Since the id tag in html matches with the name that Spring Security 
needs for config, it works now.

