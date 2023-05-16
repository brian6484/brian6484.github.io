---
layout: post
title: Error - no ParameterResolver registered for parameter error
category: Spring 
tags:
  - Spring

  
---
## Error
I got this error while running a test case. Turns out I was passing a 
method parameter that was not used anywhere in the test code block. Once 
I removed it, the error was gone.
