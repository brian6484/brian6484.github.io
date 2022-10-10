---
date: 2022-03-11 14:35:23
layout: post
title: When to add business logic to domain class, not service
description: 
category: Spring
tags:
  - Spring
  - General Knowledge

---

## Introduction
I was so accustomed to creating all my business logic in my
service class when I came across this unraveling news.

For example, 
```java
public class Item{
    private int quantity;
}

@RequiredArgsConstructor
public class ItemService{

    private final ItemRepository itemRepository;
    
    public int updateQuantity{
        //buisness logic to update quantity of Item
        //then using Item.setQuantity to update that value
        itemRepository.find
  }
}
```

## A new perspective
From object-oriented perspective, it is best to implement business
logic where the data is present in the entity. This is called **Domain Model Pattern**.

Whereas if most of the business logic is in the Service layer, it is called
**Transaction script pattern**.

```java

```
