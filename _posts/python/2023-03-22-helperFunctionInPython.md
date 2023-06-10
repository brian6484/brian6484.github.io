---
layout: post
title: Using helper functions in python and updating return value
category: Python 
tags:
  - Python
  - Data structure & Algorithms

  
---
## Error
Let's look at this helper function. I have declared count_iter outside my
function and this recursive function calls upon itself. At the last recursion,
after check() is done, we return count_iter and it would have incremented
throughout the recursion process up to like 4. We return 4 and count_iter 
value is 4. 

Then, that process is popped off the stack and the second last recursion is 
now done. At that point, it returns value of count_iter **at that context**,
which is 3. So effectively, we are updating it from true value of 4 back to 1.

Chatgpt:
Each recursive call creates a new local variable count_iter, which is separate from the original count_iter variable. As a result, the changes made to count_iter within the recursive calls do not affect the original count_iter variable.

To resolve this issue, you can remove the count_iter parameter from the check function and instead declare count_iter as a local variable within the function. Then, you can use the returned value from the recursive calls to update the count:

```python
count_iter =0

def check(queue,visited,index,cards,count_iter):
    if not visited[index]:
        queue.append(index)
        while len(queue)>0:
            index = queue.popleft()
            visited[index]=True
            count_iter+=1
            value=cards[index-1]
            check(queue,visited,value,cards,count_iter)
    return count_iter
```

Like this, 

```python
def check(queue,visited,index,cards):
    count_iter =0
    if not visited[index]:
        queue.append(index)
        while len(queue)>0:
            index = queue.popleft()
            visited[index]=True
            count_iter+=1
            value=cards[index-1]
            count_iter += check(queue,visited,value,cards)
    return count_iter
```
