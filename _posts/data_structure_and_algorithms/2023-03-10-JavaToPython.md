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


## Dictionary
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

## String
### split()
whatever_string.split() automatically splits this string into a LIST 
of substrings based on **whitespace** characters so unlike java, no 
need .split(“ “)

### no append() or pop() method in string
We cannot use append() or pop() method in strings because strings in 
Python are **immutable** unlike lists. Thus, we can achieve same functionality
via string concatentation (+) and string slicing ([start or end index 
of string you want to slice])


For example, if you want to remove the first char of string and append
to the back of the string
```python
# wrong, this is for list
# s.append(s.pop(0))

s = s[1:] + s[-0]
```

## Queue
### !queue.isEmpty() = while(queue)
More or less the same
```python
while(queue):
blabla
```

```python
visited = []
answer = []
moves = [
    (-1, -1),  # Diagonal Up-Left
    (-1, 1),   # Diagonal Up-Right
    (1, -1),   # Diagonal Down-Left
    (1, 1),    # Diagonal Down-Right
    (0, -1),   # Sideways Left
    (0, 1),    # Sideways Right
    (-1, 0),   # Up
    (1, 0)     # Down
]

def bfs(place,start_row, start_col,count):
    # queue.add(cur_pos)
    length = len(place)
    queue = [(start_row, start_col, count)]
    while(queue):
        pos = queue.pop()
        if pos[2]==2:
            return
        visited[pos[0]][pos[1]] = True
        for move in moves:
            dx , dy = move[0]+pos[0], move[1] +pos[1]
            if dx<0 or dy<0 or dx>=length or dy>= length:
                return
            elif place[dx][dy]=='0':
                queue.add(dx,dy,count+1)
            elif place[dx][dy]=='X':
                continue
            elif place[dx][dy]=='P':
                if abs(dx-pos[0]) + abs(dy-pos[1]) <=2:
                    answer.append(0)
                    return 
    answer.append(1)
        

def solution(places):
    for place in places:
        rows = len(place)
        cols = len(place[0])
        visited = [[False for _ in range(cols)] for _ in range(rows)]
        for row in range(rows):
            for col in range(cols):
                if place[row][col]=='P':
                    bfs(place,row,col,0)
    return answer
solution([["POOOP", "OXXOX", "OPXPX", "OOXOX", "POXXP"], ["POOPX", "OXPXP", "PXXXO", "OXXXO", "OOOPP"], ["PXOPX", "OXOXP", "OXPOX", "OXXOP", "PXPOX"], ["OOOXX", "XOOOX", "OOOXX", "OXOOX", "OOOOO"], ["PXPXP", "XPXPX", "PXPXP", "XPXPX", "PXPXP"]])

```

## Deque
### Declare deque
We can declare deque with no initial data, or with a starting position.
```python
hola = deque()
hola = deque([start_index, end_index])
```

### .peek() = deque[-1]
Normally before you pop it like from a stack, you need to peek at the value.
In Python, we just do deque[-1]

### pop()
If using it as a stack, pop() removes the topmost element stored in the stack
