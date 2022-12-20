---
date: 2022-07-17 14:35:23
layout: post
title: ModelAttribute annotation in MVC pattern
category: Spring
tags:
  - Spring
---
## @ModelAttribute

An object assigned with @ModelAttribute tag is automatically 
saved into Model. For Example:

```java
@PostMapping("/add")
public String addItem(@ModelAttibute("item") Item item, Model model){
  itemRepository.save(item);
  //model.addAttribute("item",item); <<this is automatically added so no need to write this
  return "items/item"
}
```

