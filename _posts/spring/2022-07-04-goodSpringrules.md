---
layout: post
title: Good Spring practice to follow
category: Spring
tags:
  - Spring
  
---

## Basic JPA 
 * If a business logic can be implemented in an entity class 
(e.g.implement in Item.java), then it is best case. This is 
called **Domain Model Pattern**.

 * In ORM, it is not good to use @Setter to set values of variables
but rather, using validation methods (usually business logic?) 
that set those values



