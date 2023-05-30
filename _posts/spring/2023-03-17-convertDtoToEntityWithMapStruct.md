---
layout: post
title: Convert dto to entity and vice versa with MapStruct
category: Spring 
tags:
  - Spring

  
---
## Dilemma 
At work and toy project, I have been manually implementing methods to 
convert DTOs to entities and vice versa by mapping each field manually.

But there is tool that can aid this burdensome process - *ModelMapper and 
Mapstruct*. But I heard Mapstruct is better in terms of API speed, no 
reflection and certain fields (like phone number that has prefix) not 
being mapped properly and thus being null values.

## Mapstruct
Firstly VERY IMPORTANT, in your gradle, lombok library has to come **FIRST** 
before mapstruct library or properties will not be mapped properly via 
mapstruct

Follow this guide very helpful: https://kth990303.tistory.com/131

As this guide says, create a GenericMapper interface that has D toDto(E e), 
E toEntity(D d), etc. Then for your entity like Log or Stats or Orders, 
make a mapper than extends this interface like

```java
Public interface OrderMapper extends GenericMapper<OrderBitchDto, Order>{
}
```

