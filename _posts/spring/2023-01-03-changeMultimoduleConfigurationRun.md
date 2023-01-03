---
layout: post
title: How to change and run different configurations in multi-module Spring project?
category: Spring
tags:
  - Spring
  
---
## Solution

For my toy project, the default configuration that the app runs
is test. But I want to change to "dev" to check if it works
before building and deploying jar file onto AWS. How do I change
the configurations?

<img src="/assets/images/posts/spring/multimodule/Screenshot%20(92).png" title="제목" width="400"/>

And under active profile, type "dev". No need to type
every dev profile like member-dev, project-dev, etc. Just dev.

