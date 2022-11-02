---
layout: post
title: JPA relationships in multi-module architecture (MSA)
subtitle: JPA
description: 
category: JPA
tags:
  - JPA
---

## JPA in normal cases
Well in normal cases, we add JPA relationships like @ManyToOne, 
@OnetoMany, etc to our primary identifiers.

For example in a unidirectional @ManyToOne relationship between Project
and Member in my toy project:

```java
public class Project extends BaseTimeEntity {

    @Id
    @GeneratedValue(strategy = IDENTITY)
    @Column(name = "project_id")
    private Long id;

    @ManyToOne
    @JoinColumn(name = "member_id")
    private Long member_id;
}
```

And we have the relevant Member entity in the same module.

## JPA in multi-module
Now, in multi-module architecture, we actually remove this 
@ManyToOne annotation because we don't have the Member entity
in the same module that contains Project entity.

So we adjust it like this:

```java
public class Project extends BaseTimeEntity {

    @Id
    @GeneratedValue(strategy = IDENTITY)
    @Column(name = "project_id")
    private Long id;
    
    @JoinColumn(name = "member_id")
    private Long member_id;
}
```

