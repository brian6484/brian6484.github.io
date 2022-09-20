---
date: 2022-06-29 14:35:23
layout: post
title: JPA's Transactional
subtitle: JPA
description: JPA
image: https://res.cloudinary.com/dm7h7e8xj/image/upload/v1559825145/theme16_o0seet.jpg
optimized_image: https://res.cloudinary.com/dm7h7e8xj/image/upload/c_scale,w_380/v1559825145/theme16_o0seet.jpg
category: Java
tags:
  - Java
  - Spring
  - JPA

---

1. JPA's @Transactional:
 * When declared at class level, @Transactional(readOnly = true) applies to every method in that class. But we don't want to readOnly for saveItem, so we declare an exception to that method with @Transactional
```java
  @Service
  @Transactional(readOnly = true)
  @RequiredArgsConstructor
  public class ItemService {
      private final ItemRepository itemRepository;

      @Transactional //this makes it readOnly=false for this saveItem method
      public void saveItem(Item item){
          itemRepository.save(item);
      }
```



