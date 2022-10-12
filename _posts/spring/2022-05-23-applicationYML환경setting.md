---
date: 2022-05-23 14:35:23
layout: post
title: yml file for setting up local, dev, production environment
description: 
category: Spring
tags:
  - Spring

---

## Intro
Without making 4 separate yml files, it is possible (and wise) to
neatly combine into 1 application.yml file effectively.

## How to set up yml and its respective environments?
```yaml
//some common yml stuff for all 3 environments

---
spring:
  profiles:
    active: local
---
spring:
  profiles:
    active: dev
---
spring:
  profiles:
    active: prod
```

In your yml file:
1) place all the settings that are shared commonly on top
2) separate it with ---
3) place your 3 environments below, separating each with ---

## When developing locally
By default, local profile is chosen and is active.
But just in case, under Run tab, select edit configurations and
type "local" to explicitly set that environment.

## Selecting the environment YOU want and deploying
First, to create a jar file, you have 2 choice.
1) Enter this command:
```yaml
./gradlew clean build
```
2) On the right tab of IntelliJ and under Gradle, select
build folder and look for build. Click and a jar file will be built,
which is stored in libs folder.

Then, how do you select the environment you want to run?
By using this command, you can select your desired environment.

```yaml
java -jar -Dspring.profiles.active=prod *.jar
```

