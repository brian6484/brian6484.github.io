---
date: 2022-09-20 14:35:23
layout: post
title: Lombok's @Builder
subtitle: Spring 
description: Spring 
category: Spring
tags:
  - Spring
  
---

I had this class. Just take a look at the order of the @Builder.
```java
@Entity
@Getter
@NoArgsConstructor(access = PROTECTED)
public class Project extends BaseTimeEntity {

    @Id
    @GeneratedValue(strategy = IDENTITY)
    @Column(name = "project_id")
    private Long id;

    @ManyToOne(fetch = LAZY)
    @JoinColumn(name = "member_id")
    private Member member;

    @Column(nullable = false)
    private String title;

    @Column
    private String category;

    @Column(nullable = false)
    private String content;

    @Lob
    @Column(nullable = false)
    private Blob contentBig;

    private Long views;

    private LocalDateTime startDate, endDate;

    private String recruitmentStatus;
    

    @Builder
    public Project(String title, String content){
        this.title = title;
        this.content=content;
    }

    //    @Builder(builderClassName = "createPostWithAll", builderMethodName = "createPostWithAll")
    @Builder
    public Project(String title, String content, Long views, LocalDateTime startDate, LocalDateTime endDate,
                   String recruitmentStatus, Member member){
        this.title = title;
        this.content = content;
        this.views = views;
        this.startDate = startDate;
        this.endDate = endDate;
        this.recruitmentStatus = recruitmentStatus;
        this.member = member;
    }
}
```

I am not sure if 1 class can have 2 @Builder patterns as such.

When I tried creating DTOs via @Builder, IDE only acknowledges variables
in the first @Builder. I want the second @Builder but variables were underlined
as red.

Turns out the order matters. I tried putting the second one on top
of the first one and it worked. But I am sure there is a better way to 
do this.

to be edited once I know:

Well my constructor 

Creating entity via constructor:
```java

```

