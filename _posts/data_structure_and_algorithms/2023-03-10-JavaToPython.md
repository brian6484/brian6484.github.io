---
layout: post
title: Python coding test prep for Java main users 
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
---
## List Comprehension
Without:
```python
def solution(n):
    for i in range(1,n):
        if n%i ==1:
            return i
```

With:
```python
def solution(n):
    return next(i for i in range(1, n) if n % i == 1)

# or
def solution(n):
  answer = min([x for x in range(1, n+1) if n % x == 1])
  return answer
```

## List 
### append() = append()
Same as java, it is append() to a list

### .index()
Tells you the index of that element. Useful when instead of storing the
index as value in a dictionary, you can just use a list and store
the elements in sequence and use .index() method

```python
eng = ['zero', 'one', 'two', 'three', 'four', 'five', 'six', 'seven', 'eight', 'nine']
answer += str(eng.index(temp))
```

### if list.isEmpty() = if not list
An empty list [] has boolean value as False. So *if not list* means that
if the list is empty. This applies to stack and deque too

```python
# if list.isEmpty()
if not list:
    
```

### sort()
The sort() method in Python **does not** accept a lambda function as a 
positional argument. Instead, it accepts the key parameter, which 
allows you to specify a function that generates a sorting key for each 
element.

```python
list.sort(key = lambda x:x[0])

//for descending order
list.sort(key=lambda x: x[0], reverse=True)
```

### reverse()
```python
bitch_list.reverse()
```

I used it when converting from base 10 to base k like
```python
def convert_to_base_k(n,k):
    digits=[]
    while n>0:
        remainder=n%k
        digits.append(remainder)
        n//=k
#     if digits is empty
    if not digits:
        digits.append(0)
    digits.reverse()
    return digits
```

### extend() to append a value multiple times to a list
```python
my_list = []
value = 42
times = 5
my_list.extend([value] * times)
print(my_list)
```

Output:
```
[42, 42, 42, 42, 42]
```

In this example, the `extend()` method is called on `my_list` with a 
list containing the value `[value] * times`. This creates a new list 
with `value` repeated `times` number of times, and then the `extend()`
method adds those elements to `my_list`.

### Improvements

```python
return [a, b]
```

Instead of 
```python
ans = []
ans.append(a)
ans.append(b)
return ans
```

### How to avoid unnecessary double for loop
I was solving https://school.programmers.co.kr/learn/courses/30/lessons/42577
when I needed one pointer in outer loop to be stationary while I compared
with the rest of the elements in the list with another pointer in inner loop.
Like this

```python
def solution(phone_book):
  phone_book.sort()
  for i in range(len(phone_book)):
    for j in range(i+1,len(phone_book)):
      if phone_book[i+1].startswith(phone_book[i]):
        return False
  return True
```

This passes tests but not efficiency tests because double for loops is O(n^2)
time complexity. Now how do we do this with 1 for loop? We actually
use the same 1 pointer (i) but we give it some limits like

```python
def solution(phone_book):
    phone_book.sort()
    for i in range(len(phone_book)-1):
        # for j in range(i+1,len(phone_book)):
        if phone_book[i+1].startswith(phone_book[i]):
            return False
    return True
```

Notice that to avoid index going out of range, pointer i stops 1 index less
than the final possible index of list. 

[Fix 25th June] Wait actually this doesnt traverse all the rest of the elements
in the list. It just checks the one on the right and that is it.



