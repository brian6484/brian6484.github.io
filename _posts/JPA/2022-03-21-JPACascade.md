---
date: 2022-03-21 14:35:23
layout: post
title: JPA cascade
subtitle: JPA
description: 
category: JPA
tags:
  - JPA
---

## JPA cascade
We can use this 영속성 전이 transitive persistence functionality when we 
make a specific entity as managed state by EM and want the related 
entities to be managed as well. For example, when we save parent entity, 
we want to save child entity at the same time for convenience.

BTW, remember that for JPA to save entities, **ALL related entities 
have to be in managed state**

Without cascade, we need to do for example in bidirectional:

```java
em.persist(parent)

child1.setParent(parent) //child -> parent 연관관계 설정
parent.getChildren().add(child1) //parent -> child 연관관계 설정
em.persist(child)
```

But with cascade like
```java
@OneToMany(mappedBy=”parent”, cascade = PERSIST)
Private List<Child> children = new ArrayList<>();

child1.setParent(parent) //child -> parent 연관관계 설정
parent.getChildren().add(child1) //parent -> child 연관관계 설정
em.persist(parent)

//no em.persist(child)
```

remember that for JPA to save entities, **ALL related entities have to be 
in managed state**. Without cascade, we have to manually separately make 
parent and child entities as managed by persisting them. But using 
CascadeType.PERSIST, when parent entity is in managed state by 
persisting, all the related entities (child entities in this case) are 
all converted to managed state (persisted) in 1 go. Cascade provides the 
convenience that when an entity is persisted, other related entities are 
persisted also.

**Same logic for REMOVE**

We can put parameter ALL that has all properties of cascade

## CascadeType.ALL
 * cascade = CascadeType.ALL declared for orderItems and delivery, which means when order is persisted, its collection which includes orderItems and delivery entity are also persisted into database. So there is no need to create those 2 repositories.

 * cascade = CascadeType.ALL should be used when entity is called only by one final entity like order. If it is called by more than 1 entity, then should not be used.

```java
orderRepository.save(order)
// no need to save other entities that are linked with order like
//memberRepository.save(member);
//itemRepository.save(item);

```

## difference between cascade.remove and orphanRemoval = true

They both manage persistence of related entities when a parent entity is 
removed. However there is a difference

Cascade.remove **propagates** (전이) removal operation from parent to 
connected child entities. Useful to ensure all related entities are 
deleted when a parent entity is deleted

Orphan removal removes child entity when they are no longer associated 
with a parent entity. It means when I remove a child entity from a 
parent’s collection, that child entity will be deleted from DB. Useful 
to ensure child entities sare persisted **only** if they are associated 
with a parent entity


## all + orphanRemoval = true
Through parent entity, we can control 생명주기 lifecycle of child entity. For example if we want to remove child, we can remove via parent

Parent parent = em.find(Parent.class, parentId)
parent.getChildren().remove(removeObject)
