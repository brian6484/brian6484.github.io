---
layout: post
title: defaultdict(list) vs just dictionary
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
---

## Difference
The difference between `graph = {}` and `graph = defaultdict(list)` lies in the behavior when accessing a non-existing key in the dictionary.

1. `graph = {}`:
   When using `graph = {}` to create a dictionary, if you try to access a key that does not exist in the dictionary, a `KeyError` will be raised. For example:

   ```python
   graph = {}
   print(graph['key'])  # Raises KeyError: 'key'
   ```

   In this case, accessing a non-existing key raises an error since the default behavior of a regular dictionary is to raise a `KeyError` when accessing a key that doesn't exist.

2. `graph = defaultdict(list)`:
   When using `graph = defaultdict(list)` to create a dictionary, it creates a special kind of dictionary where accessing a non-existing key will not raise an error. Instead, it will create a new entry for that key and initialize it with a default value, which in this case is an empty list (`[]`). For example:

   ```python
   from collections import defaultdict
   
   graph = defaultdict(list)
   print(graph['key'])  # Outputs an empty list: []
   ```

   In this case, accessing a non-existing key (`'key'`) creates a new entry with an empty list as the default value. This can be useful when working with graphs or other data structures where you want to automatically initialize new entries with a specific default value.

So, the main difference is that `defaultdict(list)` provides a default value for non-existing keys, while a regular dictionary (`{}`) raises a `KeyError` when accessing a non-existing key.
