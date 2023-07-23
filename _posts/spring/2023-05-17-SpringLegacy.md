---
layout: post
title: Spring Legacy and some precautions
category: Spring 
tags:
  - Spring

  
---
## Issue
(Spring Legacy) Always take note of your output directory (배포 파일). 
For example, I had 4 ojdbc files in my output directory file so there were 
conflicts of multiple versions. JVM always executes the one that is the 
“oldest” so even though I added the correct new one, it is not updated 
properly. I thought I was adding it properly via Library in my Project 
Structure but that is not the case. You have to check your output directory, 
which can be found in Project Sturcutre’s artifact tab.
