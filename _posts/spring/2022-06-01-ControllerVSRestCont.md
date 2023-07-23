---
layout: post
title: Spring Controller and difference between Controller VS RestController
category: Spring
tags:
  - Spring
  
---
## @Controller
### Issue
For registering new users, I had aPostMapping controller of register 
function. I wanted whatever fields of UserRegisterDto were wrong, I want 
to have them printed out on the page itself. But whenever there was an 
error, i get a 404 page but the error appeared on the run console.

Initial code:
````java
UserResponseDto userResponseDto = userService.register(userRegisterDto)
````


### Solution
```java
userService.register(userRegisterDto)
```

I am not sure how it fixes the error so I will get back to this post.

## @RestController
@RestController is effectively @Controller + @ResponseBody combined together.

## @Controller VS @RestController

If return value of @Controller is String, it is rendered as *view* but 
for @RestController, return value is inserted into HTTP message body. 









