---
date: 2022-04-27 14:35:23
layout: post
title: JsonIgnore annotation
description: 
category: Spring
tags:
  - Spring

---

## How not to expose an entity's field?
Let's consider this entity:
```java
@Entity
@Data
public class Member{
    
    @Id @GeneratedValue
    private Long id;
    
    private String name;
    
    //@JsonIgnore
    @OneToMany(mappedBy= "member")
    private List<Order> orders = new ArrayList<>();
}
```

If we get a list of members, we see that we bring the list of orders with it in the
json data.

If we want to stop orders from being tagged along when querying for members,
add @JsonIgnore annotation to the field you don't want to bring up.





