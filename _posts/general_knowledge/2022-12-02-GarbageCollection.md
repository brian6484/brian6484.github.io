---
layout: post
title: GarbageCollection in Java (feat. stack and Heap)
description:
category: General Knowledge
tags:
  - General Knowledge
  - Head First Java
---
숨참고 love dive~

## Garbage Collection
We have talked about [stack and heap](https://brian6484.github.io/general%20knowledge/2022/02/18/GarbageHeapAndStack.html)
and how heap stores all the objects that are created, and
stack stores the methods and local variables.

But what happens when we destroy objects once we are done using
them?

Unlike C/C++ languages, Java does not require developers 
to explicitly free objects. It is also a great advantage 
of the Java language. Deleting unused objects from memory
is called Gargabe Collection (GC), and GC is performed by 
the JVM.



