---
layout: post
title: Does HashMap allow duplicate keys when putting same key with different value?
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
---

## Explanation
[This reference](https://stackoverflow.com/questions/1669885/what-happens-when-a-duplicate-key-is-put-into-a-hashmap)
explains really well.

HashMap does NOT allow duplicate keys so when we try to 
```java
Map mymap = new HashMap();
mymap.put("1","one");
mymap.put("1","not one");
mymap.put("1","surely not one");
System.out.println(mymap.get("1"));
```

We get "surely not one", the latest value. Why?

>The map simply drops its reference to the value. 

And by definition, put *replaces* the previous value associated with
the key in HashMap.
