---
layout: post
title:  Binary Search and practice questions
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
---

## Binary search original template
  


## Practice questions


### 입국심사
https://school.programmers.co.kr/learn/courses/30/lessons/43238

my correct solution. Remember I said binary search is literally guessing
the answer value and seeing if all can be processed within that answer
value.

```python
def solution(n, times):
    start = 0
    end = 1000000000000000000
    answer = 0
    
    while start <= end:
        mid = (start + end) // 2
        peeps = sum(mid // i for i in times)
        
        if peeps >= n:
            end = mid - 1
        else:
            start = mid + 1

    return start
```

Notice here we are returning start instead of start-1 unlike our
previous example. We return start because it represents the smallest 
possible time that allows processing n people, which is what we were 
searching for.

### 징검다리 건너기
https://school.programmers.co.kr/learn/courses/30/lessons/64062

initial wrong solution where  I was setting wrong condition for if
```python
def solution(stones, k):
    start = 0
    end = 200000000

    while start <= end:
        mid = (start + end) // 2
        temp = [0 if i - mid < 0 else i - mid for i in stones]
        hola = 0
        flag = False
        for num in temp:
            if num <= 0:
                hola += 1
                if hola > k:
                    flag = True
                    break
            else:
                hola = 0
        if flag:
            end = mid - 1
        else:
            start = mid + 1

    print(start)
    return start
```

It should be if hola >= k. This is because let's say if we have k=3,
once we encounter 3 consecutive 0s, then our hola value is 3 and greater
and that is condition for our flag. It is not hola>3 just look at the
question diagram. Flag should be raised when we see k or more times of
consecutive 0s.

my question to gpt

`ah ok so the way that i was count hola is that if k is 3 and hola is incremented until value 3, that means there are 3 consecutive 0s already which means we cannot continue `

reply back was

Yes, exactly! In this problem, `hola` represents the number of consecutive 0s encountered in `temp`. When `hola` becomes equal to or greater than `k`, it means that you have found a position where it is not possible to continue jumping `k` consecutive stones, as there are already `k` or more consecutive 0s.

By checking `hola >= k`, you ensure that you detect this condition correctly and stop the loop when it is not possible to continue jumping `k` consecutive stones.

my fixed solution
```python
def solution(stones, k):
    start = 0
    end = 200000000

    while start <= end:
        mid = (start + end) // 2
        temp = [0 if i - mid < 0 else i - mid for i in stones]
        hola = 0
        flag = False
        for num in temp:
            if num <= 0:
                hola += 1
                if hola >= k:
                    flag = True
                    break
            else:
                hola = 0
        if flag:
            end = mid - 1
        else:
            start = mid + 1

    print(start)
    return start
```

gpt sensei solution:
```python
def solution(stones, k):
    start = 1
    end = max(stones)

    while start <= end:
        mid = (start + end) // 2
        count = 0
        flag = False

        for stone in stones:
            if stone - mid <= 0:
                count += 1
            else:
                count = 0

            if count >= k:
                flag = True
                break

        if flag:
            end = mid - 1
        else:
            start = mid + 1

    return start
```

This is better cuz end is set more efficiently. Setting max(stones) is better
as less iterations are needed.


