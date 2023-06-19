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
But if you are using it as queue, use popleft()

### append((whatever elements in a list))
Unlike list, deque's append is different. In list, we do .append([list of elements])
but in deque, we don't use the square brackets. 

## Collections
### Counter
Counter counts the frequency of elements in an iterable. It is a subclass of
dict class and so inherits all funtionalities of dict.
```python
my_list = [1, 2, 3, 1, 2, 1, 3, 4, 5, 4, 4]
counter = Counter(my_list)

print(counter)
# Output: Counter({1: 3, 4: 3, 2: 2, 3: 2, 5: 1})

print(counter[1])
# Output: 3
```

#### Comparing Counter with dict with ==
You can straight away compare your dict with Counter via == whether 
```python
for i in range(len(discount) - 9):
    if dict_super == Counter(discount[i:i+10]):
        answer += 1
```
