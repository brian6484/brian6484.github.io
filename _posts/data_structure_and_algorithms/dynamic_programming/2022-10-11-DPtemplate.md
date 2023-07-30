---
layout: post
title: Dynamic Programming explained
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
---

## Approach
1) Remember to ALWAYS set default values as starting points
for our DP iteration (e.g. dp[0]= sth)

## Template
Let's take [this Fibonnaci example](https://leetcode.com/problems/fibonacci-number/solutions/215992/java-solutions/?orderBy=most_votes)

It is good to get the logic first and start from recursive,
then implement memoisation for DP. Lastly, iterative solution
would be the best.

Another example is [house robbers](https://leetcode.com/problems/house-robber/solutions/156523/from-good-to-great-how-to-approach-most-of-dp-problems/)

## Practice questions
### 연속 펄스 부분 수열의 합
https://school.programmers.co.kr/learn/courses/30/lessons/161988

I referred to https://lottegiantsv3.tistory.com/168 but the intuition is 
better explained in https://magentino.tistory.com/110.

### Original thought 
My original thinking was calculating maximum sum of consecutive subsequences
using Kadane's algorithm. But it didn't work out so I googled for more insight.

### DP thinking
So instead of considering all possible cases of this pulse sequence, we
can just create 2 pulse sequences of those 2 given patterns. If we do 
완전탐색 we will get O(n^2) time complexity so it will cause runtime error.
Instead, we can use DP but what condition do we set?

First, we create a 2d list DP, where dp[0] will contain the first pulse
sequence that follows pattern (1,-1,1) and dp[1] will contain the second
pulse that follows pattern (-1,1,-1). Then, dp[whichever pulse sequence][index] will be the maximum
sum of a subsequence that must end the subsequence with that index. 

So we have 2 choices - if the previous subsequence sum(dp[whatever pulse sequence][index-1]) and our current value
at the current index is bigger than just our current value at current index,
we take the bigger value. But if subsequence we had was really negative, then
we are better off starting fresh with our current value at current index.

So the relation is

`DP[0][index]  = max(current_value, current_value + dp[0][index-1])`

`DP[1][index]  = max(current_value, current_value + dp[1][index-1])`

my correct solution 웬일로?
`````python
def solution(sequence):
    length = len(sequence)
    dp = [[0 for _ in range(length)] for _ in range(2)]
    #     dp[we have 2 possible lists with 1,-1,1 or -1,1,-1 pattern][sum up till which index]
    dp[0][0]= sequence[0]
    dp[1][0]=sequence[0]*-1
    answer=max(dp[0][0], dp[1][0])
    for index,value in enumerate(sequence):
        if index==0:
            continue
        if index%2==0:
            dp[0][index] = max(value,value+dp[0][index-1])
            dp[1][index] = max(value*-1,value*-1+dp[1][index-1])
        else:
            dp[0][index] = max(value*-1,value*-1+dp[0][index-1])
            dp[1][index] = max(value,value+dp[1][index-1])
        answer=max(answer, max(dp[0][index],dp[1][index]))
    return answer
`````

### Better solution
refer to https://magentino.tistory.com/110
We can actually just use the same sequence and return absolute 
values of the minimum and maximum subsequence sum because by taking the
abs(), you have same effect as reversing that pulse sequence pattern. (1,-1,1 -> -1,1,-1)
