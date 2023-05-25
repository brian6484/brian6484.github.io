---
layout: post
title: Python coding test prep for Java main users 
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
---

## Dictionary
### dict.keySet() = dict.items()
* Java Dictionary's keySet(), which consists of both key and value, is
same as .items()
```python
for key,value in dict.items():
  
# Set<String> keySet = map.keySet();
# for (String key : keySet) {
#   System.out.println(key);
# }
```

### dict[key] = set()
* If you want to set a set for a specific key so that no duplicate values 
are allowed for that key, declare it like this
```python
dict[key] = set()
dict[key].add(value1)

```
