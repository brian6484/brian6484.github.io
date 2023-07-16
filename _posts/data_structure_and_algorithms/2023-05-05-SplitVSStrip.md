---
layout: post
title: Difference between split() and strip() in Python
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
---

## Difference
split and strip has different usages. Split splits string into a `list` of 
substrings while strip removes any *leading or trailing whitespaces* like 
```python
String sample = "   hola  "
```

## split()
### maxsplit parameter
```python
.split(maxsplit=1)
```
This maxsplit parameter determines max number of splits to perform. 
Default is -1 but if you set value like 1, split operation will be done
**only once** and hence, maxsplit (literally). So it will create at most 
2 substrings. If I have a string like 
```python
hey = "I love eating pizza and pasta."
print(hey.split())          # Output: ['I', 'love', 'eating', 'pizza', 'and', 'pasta.']
print(hey.split(maxsplit=1))  # Output: ['I', 'love eating pizza and pasta.']
```




