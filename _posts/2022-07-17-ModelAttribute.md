---
date: 2022-07-17 14:35:23
layout: post
title: ModelAttribute
subtitle: Spring 
description: Spring 
image: https://res.cloudinary.com/dm7h7e8xj/image/upload/v1559825145/theme16_o0seet.jpg
optimized_image: https://res.cloudinary.com/dm7h7e8xj/image/upload/c_scale,w_380/v1559825145/theme16_o0seet.jpg
category: Java
tags:
  - Java
  - Spring
  
author: Jeonghwan Lee
---

1. @ModelAttribute

* An object assigned with @ModelAttribute tag is automatically saved into Model. For Example:

```java
@PostMapping("/add")
public String addItem(@ModelAttibute("item") Item item, Model model){
  itemRepository.save(item);
  //model.addAttribute("item",item); <<this is automatically added so no need to write this
  return "items/item"
}
```
