---
layout: post
title: Difference between StringBuffer and StringBuilder
subtitle: 
description:
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
  - Head First Java
---
# A note on Strings
String is immutable so it cannot be modified once it is 
instantiated. To modify it, we can create and use StringBuffer
or StringBuilder

## Difference
StringBuffer is actually thread-safe in a multi-threaded 
environment by supporting the synchronisation. It means
2 threads cant call the methods of StringBufffer at the
same time.Btw, since String also has immutability, it also has stability 
(thread-safe) in a multi-threaded environment.

Conversely, StringBuilder does not support synchronisation, 
so it is not suitable for use in a multi-threaded 
environment, but performance in a single thread is superior
to StringBuffer as it does not consider synchronisation.




