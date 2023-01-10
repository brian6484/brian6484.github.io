---
layout: post
title: Difference between Spring filter and interceptor?
category: Spring
tags:
  - Spring

---
## Diff
There is a difference at the time of execution.
Filter is executed before a request goes to the dispatcherServlet, and an interceptor is executed before a request goes to the controller.

Normally, to use them commonly, we just use them to process
tasks before entering controller but still, there is a
difference at the time they are actually executed.
