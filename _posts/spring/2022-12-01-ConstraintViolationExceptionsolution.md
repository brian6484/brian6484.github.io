---
layout: post
title: Spring ConstraintViolationException error solution
category: Spring
tags:
  - Spring

---

When I was making a test case for saving a project post
in my ProjectRepository, this error popped up: 

org.springframework.dao.DataIntegrityViolationException: could not execute statement; SQL [n/a]; constraint [null]; nested exception is org.hibernate.exception.ConstraintViolationException: could not execute statement

Dafuq? I googled and they were talking about PK제약조건이 중복되어서 생기는 오류.

But for my case, one of my attributes (Blob contentBig) in Project class was @Column(nullable=false)
and I **did not put sample data** for it while testing. Either allowing it to 
accept null values or adding sample data is the solution.


