---
layout: post
title:  How to set JDK in bash profile in linux
category: Linux
tags:
  - Linux
---

## Solution

I was confused with how to set jdk in my bash profile. Do I find a 
specific .jdk file or just a jdk folder?

## Solution
When I depressed my compressed jdk files with tz format, some folders 
looked like openlogic-openjdk-bla but the official jdk that I downloaded 
from Oracle looked like jdk1.8.0_371. This is the valid one and we just 
need to set the entire folder as the environment variable in the 
bash profile like

`Export JAVA_HOME=/home/brian/jdk/jdk1.8.0_371`
