---
date: 2022-03-21 14:35:23
layout: post
title: JPA cascade
subtitle: JPA
description: 
category: JPA
tags:
  - JPA
---

## JPA cascade

## CascadeType.ALL
 * cascade = CascadeType.ALL declared for orderItems and delivery, which means when order is persisted, its collection which includes orderItems and delivery entity are also persisted into database. So there is no need to create those 2 repositories.

 * cascade = CascadeType.ALL should be used when entity is called only by one final entity like order. If it is called by more than 1 entity, then should not be used.

```java
orderRepository.save(order)
// no need to save other entities that are linked with order like
//memberRepository.save(member);
//itemRepository.save(item);

```



