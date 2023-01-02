---
layout: post
title: Authorisation with Redis
category: Redis
tags:
  - Redis
  - 
---

## Why Redis?
Let's look at this example:
```java
Long memberId = tokenProvider.getMemberIdByToken(jwtToken);
Member member = memberRepository.findById(memberId);
```

When there is minor or no change to DTOs, it is not worth and 
computationally unnecessary and expensive to pass DTO to DB and 
authorise every time. We know that this member is really that
authorised member so can we somehow improve this?

## Possible solution
1) When issuing JWT token for authorisation, save the memberDto in
redis as well. Redis requires key-value format so key would be
JWT token and value is memberDto. (key,value) is (jwtToken,memberDto)

2) When another HTTP request is done, if there is such memberDto value,
we can just return the JWT token to the user? (lemme check on this,
so we don't check the JWT token? and how about searching the DB?)

