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


## In 양방향 relationships and using Entity directly (a NO NO)
Let's say member and project is @OneToMany. When we do JPA query for 
either of the 2, it directs to each other in an infinite loop.

To prevent this, we **must** add @JsonIgnore to one of the 2 entities
to stop this loop.

But anyway, you should not be exposing your entities directly
but using DTOs so take this as a reference.

