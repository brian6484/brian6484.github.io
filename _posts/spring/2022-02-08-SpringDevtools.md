---
date: 2022-02-08 14:35:23
layout: post
title: Spring Devtools
subtitle: Spring
description: 
category: Spring
tags:
  - Spring
---

## Introduction
Every time you make a change to HTML file, we need to restart
the server to see the changes. But once you import Devtools, it
saves all the trouble.

*Update October 5th 2022* This doesn't work just for HTML files,
you can recompile controllers as well without restarting server.

## How to set up
Import the dependency into your build.gradle file and remember to 
press that elephant *wink* to update
```yaml
dependencies {
    compileOnly("org.springframework.boot:spring-boot-devtools")
}
```

### Before 
You can see that before implementing Devtools, it is marked as [ Main].
```yaml
2022-10-05 14:13:38.067  INFO 16968 --- [  Main] jpabook.jpashop.JpashopApplication       : Starting JpashopApplication using Java 11.0.15 on DESKTOP-55D50QU with PID 16968 (C:\Users\Brian\Documents\Coding\jpashop\out\production\classes started by Brian in C:\Users\Brian\Documents\Coding\jpashop)
2022-10-05 14:13:38.068  INFO 16968 --- [  Main] jpabook.jpashop.JpashopApplication       : No active profile set, falling back to 1 default profile: "default"
```

### After
Now, it is marked as [   restartedMain] and there are 2 more additional
lines marked as "DevToolsPropertyDefaultPostsProcessor"
```yaml
2022-10-05 14:13:38.067  INFO 16968 --- [  restartedMain] jpabook.jpashop.JpashopApplication       : Starting JpashopApplication using Java 11.0.15 on DESKTOP-55D50QU with PID 16968 (C:\Users\Brian\Documents\Coding\jpashop\out\production\classes started by Brian in C:\Users\Brian\Documents\Coding\jpashop)
2022-10-05 14:13:38.068  INFO 16968 --- [  restartedMain] jpabook.jpashop.JpashopApplication       : No active profile set, falling back to 1 default profile: "default"
2022-10-05 14:13:38.097  INFO 16968 --- [  restartedMain] .e.DevToolsPropertyDefaultsPostProcessor : Devtools property defaults active! Set 'spring.devtools.add-properties' to 'false' to disable
2022-10-05 14:13:38.097  INFO 16968 --- [  restartedMain] .e.DevToolsPropertyDefaultsPostProcessor : For additional web related logging consider setting the 'logging.level.web' property to 'DEBUG'
```

## How to use
Go to your HTML file, and once you made your changes:
Go to Build tab, and press on "Recompile xxx.html"





