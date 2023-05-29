---
layout: post
title: List as method argument and parameter in Python
category: Python 
tags:
  - Python
  - Data structure & Algorithms

  
---
## Explained
I was confused with Python cuz in Java, you **need** to delcare the data type
in your method parameter like
```java
public int hola(int bitch, List<Integer> list){
    
  }
```

But in Python, be it list or any other data types, you don't need to.

```python
# you can call your bfs function like this, inserting method argument of 
# place and list of row,col and 0
bfs(place,[row,col,0])

# and as declared in your bfs function
def bfs(place,pos):
```

In your example, the bfs function takes two arguments: place and pos. The 
pos argument is expected to be a list, as indicated by the usage of 
pos[0], pos[1], and pos[2] within the function.
