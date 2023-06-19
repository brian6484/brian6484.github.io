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

### iterating through highest keys in descending order
You can iterate through the highest keys in a dictionary by using the 
`sorted()` function with the `keys()` method of the dictionary.

```python
my_dict = {'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5}

# Get the highest keys in descending order
highest_keys = sorted(my_dict.keys(), reverse=True)

# Iterate through the highest keys
for key in highest_keys:
    value = my_dict[key]
    print(key, value)
```

Output:
```
e 5
d 4
c 3
b 2
a 1
```

So you are effectively not sorting the dictionary itself, but smartly 
sorting the keys in descending order **in a list** separately and 
passing that key to dict to get the value.



