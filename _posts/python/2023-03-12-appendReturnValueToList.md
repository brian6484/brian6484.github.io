---
layout: post
title: Appending return value to list in Python
category: Python 
tags:
  - Python
  - Data structure & Algorithms

  
---
## Appending return value to list in Python
Let's take a look at this example where I am doing a DFS search where 
if a certain condition is met like if node is already visited or dx dy is
out of the grid, I want to return False. If it passes all checks, it is worthy
to return True. I just want **one** return value for that one particular DFS search
point.

```python
from collections import deque
ans=[]

def bfs(p, idx):
    while queue:
    #   if some condition
        return False
    return 1

def solution(places):
    for place in places:
        for row in range(len(places[0])):
            for col in range(len(places)):
                if places[row][col]=='P':
                    ans.append(bfs(place,[row,col,0]))
    return ans
```

The ans that I get is  [1,1,1,1,1,1,false,false,false,1,false,false,false,1
,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1] where as the correct answer is
[1,0,1,1,1]. As you can see 5 values are added to my ans list but I only want
one boolean value to check if DFS search is True or False.

Actually, this way appends each return value everytime it is computed. What
we need to do is *overwrite* the return value.

Update at midnight 29th.
Actually, I was deeply mistakened
1) it should be place[row][col] not places.
2) As you see in the most innerloop iteration, a value is produced for 
**each** column as dfs search is done on each grid if its value is 'P' so 
since there are 5 'P's, 5 values are produced. If just one of these 5 
values is False, it means BFS search return values is False and I want to mark 
the value as False. In this case we can use a flag and see if there is just one
value that comes in as False, we flag it. Then, according to if this flag
has been raised or not, it shows whether BFS search is successful or not and
we can append just 1 value at the 'place' level according to the flag.

The correct way is 
```python
def solution(places):
  # global ans
  for place in places:
    flag =1
    for row in range(len(places[0])):
      for col in range(len(places)):
        if place[row][col]=='P':
          val = bfs(place,[row,col,0])
          if val == False:
            flag =0
    ans.append(1 if flag==1 else 0)
  return ans
```
