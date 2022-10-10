---
date: 2022-04-19 14:35:23
layout: post
title: Prevent multiple ways to initialise/create Object
description: 
category: Spring
tags:
  - Spring

---

## Prevent multiple ways to create Object
When there are multiple ways to create Object - either via constructor or a custom-made
method, it can cause confusion when additional fields are added and makes it hard to maintain.

For example:

```java
//
public static OrderItem createOrderItem(your parameters){
    //code to create this object
  }

// and in your Service,
OrderItem orderItem = OrderItem.createOrderItem(your parameters);

//but you can also create via constructor like this in your Service
OrderItem orderItem = new OrderItem(ur parameters);
```

So effectively, if this is not controlled, it is hard to maintain.

## Solution
If you have created a custom-made method to create an object, you want to block
this constructor way of creating object. One way is to create a protected constructor.

```java
public class OrderItem(){
    protected OrderItem(){
        
    }
}
```

This can be further optimised via Lombok:
```java
@NoArgsConstructor(access = PROTECTED)
public class OrderItem(){
    //blabla
}
```
