---
layout: post
title: Dictionary useful methods and practice questions
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
---
  
## Dictionary
### Counter 
Counter is a subclass of dictionary and thus has all methods of dictionary.
We can actually compare Counter object with dictionary with == like

```python
for i in range(len(discount)-9):
    if dic == Counter(discount[i:i+10]): 
        answer += 1
```



### dict.keySet() = dict.items()
Java Dictionary's keySet(), which consists of both key and value, is
same as .items()
```python
for key,value in dict.items():
  
# Set<String> keySet = map.keySet();
# for (String key : keySet) {
#   System.out.println(key);
# }
```

### dict.contains(key) = if key in dict
Checking if dict contains this key can be done via
```python
if key in dict:
if key not in dict:

# if dict.contains(key):
```

### dict[key] = set()
If you want to set a set for a specific key so that no duplicate values
are allowed for that key, declare it like this
```python
dict[key] = set()
dict[key].add("hi")


# Map<String, Set<Integer>> map = new HashMap<>();
# map.put("key1", new HashSet<>());
# map.put("key2", new HashSet<>());
```
