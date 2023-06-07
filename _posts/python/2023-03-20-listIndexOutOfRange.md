---
layout: post
title: List index out of range (list initialised wrong!)
category: Python 
tags:
  - Python
  - Data structure & Algorithms

  
---
## Error
Actually this all arises from initialised a list in the wrong way.

```python
parent = [0 * (length+1)]
for i in range(1,length+1):
    parent[i]=i
```

The expression 0 * length+1 is a **single element** '0'. So when I try to
access beyond the first index, I get the "index out of range error".

The right way should be 
```python
parent = [i for i in range(length+1)]
```
