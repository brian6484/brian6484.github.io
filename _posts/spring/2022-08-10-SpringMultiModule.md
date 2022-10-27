---
layout: post
title: Spring Multi-module structure
description: 
category: Spring
tags:
  - Spring

---

## Intro
Place common code in the common module that can be shared by other
modules.

## ApplicationContext error when testing
When creating test cases within my module, I encountered an
ApplicationContext error. That is strange, I am getting token errors
like GoogleOAuth that I didn't even use in my module.

Well, even in tests, our module relies only on the common module
and not other modules.

Thus, solution is to remove other modules' dependencies in build.gradle.

```yaml
jar { enabled = true }

dependencies {
  //remove the other modules' dependencies
#    testImplementation project(':module-member')
#    testImplementation project(':module-skill')
    testImplementation project(':module-common')
}
```

