---
layout: post
title: Spring Events and what are they?
subtitle: Spring
category: Spring
tags:
  - Spring
---

## Why do we use @EventListener?
We use it to separate layers of business logics that are highly 
dependent on one another.

For example, let's say when A Service runs A business logic, it
requires B Service's B business logic. In this case, we need to 
DI B Service into A service, placing B logic into A logic. This is
not ideal because it is becoming reliant on other Service.

To solve this increasing connectivity, we create EventHandler, which is
a layer, that separates and loosens this connectivity.

A 서비스의 a 로직 실행 -> 이벤트 발행 -> B 서비스의 b 로직 실행

이렇게 되면 A 서비스는 B 서비스의 변경사항과 관련없이 수정이 필요없게 됩니다.

## Example
sad

## Reference
https://shinsunyoung.tistory.com/m/88
https://sunghs.tistory.com/m/139
