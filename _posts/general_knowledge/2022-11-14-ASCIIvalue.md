---
layout: post
title: ASCII value in Java and how to store in array of size 128 or 256?
category: General Knowledge
tags:
  - General Knowledge
  - Java
---
## ASCII value
ASCII represents a numeric value for each character, like 65 is a value of A.
ASCII is a 7-bit character set having 128 characters, i.e., from 0 to 127.

## Storing in integer array of size 128
```java
int[] array = new int[128];
for(int i=0; i<s.length();i++){
    array[s.charAt(i)] = i+1;
  }
```

Using string.charAt() method, we can store each character's
ASCII value in an integer array like so.



