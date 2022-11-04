---
layout: post
title: Spring Boot + JPA following Java's camelCase or DB's underscore when naming fields
subtitle: JPA
description: 
category: JPA
tags:
  - JPA
---

## Discussion
Let's see this example:
```java
@Entity
public class Member{
    @Id @GeneratedValue
    @Column(name="member_id")
    private Long id;
    
    private LocalDateTime orderDate;
}
```

Remember LocalDateTime is specially recognised by JPA and adds that
field to be mapped to the entity?

Anyway, look at this field name orderDate. The DB prefers name to be
ORDER_DATE or order_date with underscores. But Java prefers camelCase
like orderDate.

So how should we name it? We optimally want to name it how the DB
wants with underscores.

Actually Spring Boot, the latest versions that we are using, addresses this
issue. It **automatically** takes any Java's camelCase names and 
edits it to the conventional naming way of DB.

So in this case, even without @Column(name="order_date), Spring Boot
automatically changes the name to order_date and maps it to the entity
and saves it to DB.

Cool!



