---
layout: post
title: How to upload files to S3 on Spring Boot project (from set-up to controller)
subtitle: Java 
description: Java
category: Java
tags:
  - Java
  - Head First Java
---

## Intro
[This easy reference](https://devlog-wjdrbs96.tistory.com/323) is
an easy guide but it provides really basic logic so I plan to add on
more complex logic here.

## Make S3 bucket on AWS
One thing to note is don't block all public access because if we do,
we can't access it from our Spring Boot project.

Once S3 has been made, make sure your IAM policy includes S3FullAccess
policy or some sort of S3 policy attached to your role.

**Very important** If you do have S3 access, you will have these 2 
important fields - accessKey and secretKey in your IAM role that 
are needed when setting up .yml file.



