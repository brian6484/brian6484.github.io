---
layout: post
title: Appending return value to list in Python
category: Python 
tags:
  - Python
  - Data structure & Algorithms

  
---
## Lists are mutable objects in Python
Take a look at this example
```python
nums = [1,2,3]
visited = [False for _ in range(len(nums))]
ans = []
path =[]

def dfs(nums,path,visited):
    for i in range(len(nums)):
        if len(path) == len(nums):
            # issue here
            ans.append(path)
            return
        if not visited[i]:
            visited[i]=True
            path.append(nums[i])
            dfs(nums,path,visited)
            path.pop()
            visited[i]=False
            
dfs(nums,path,visited)
print(ans)
```

When I am done with DFS search, I append the path [1,2,3] to my answer list.
But when this code runs, my ans is a list of empty lists. What happened?

In python, lists are *mutable objects*, which means they can be modified 
along the way. When I try appending a list to another list, I am not appending
the actual copy of that list but a **reference** to the original list. 
This means that any changes made to the original list will also be 
reflected in the appended list since they both refer to the same object.

In my code, when I append the path list to ans using ans.append(path), 
I am appending a **reference** to the path list. Then, when I later 
modify the path list by popping elements or backtracking, those changes 
are also reflected in the lists already appended to ans.

## Solution
So instead of appending a **reference**, add an actual copy of the path list.

```python
    if len(path) == len(nums):
        ans.append(path.copy())
        return
```

To avoid this issue, you need to create a copy of the path list before 
appending it to ans. In Python, you can create a shallow copy of a list 
using the copy() method. The copy() method creates a new list object with 
the same elements as the original list.

By using ans.append(path.copy()), you create a separate copy of the path 
list each time it needs to be appended to ans. This ensures that each 
list in ans is independent and unaffected by subsequent modifications 
to the path list.
