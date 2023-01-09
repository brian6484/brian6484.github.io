---
layout: post
title: How to save time in for loop?
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
---
## Issue
I was solving this [leetcode](https://leetcode.com/problems/integer-break/)
and my code is:
```java
class Solution {
    public int integerBreak(int n) {
        int[] dp = new int[n+1];
        dp[1]=1;
        for(int i=2; i<=n; i++){
            for(int j=1; j<=i/2; j++){
                dp[i] = Math.max(dp[i], Math.max(j,dp[j]) * Math.max(i-j, dp[i-j]));
            }
        }
        return dp[n];
    }
}
```

Apparently, we can save half of the time by changing the inside loop
via j < i to 2*j <= i

```java
public int integerBreak(int n) {
    int[] dp = new int[n + 1];
   dp[1] = 1;
   for(int i = 2; i <= n; i ++) {
       for(int j = 1; 2*j <= i; j ++) {
           dp[i] = Math.max(dp[i], (Math.max(j,dp[j])) * (Math.max(i - j, dp[i - j])));
       }
   }
   return dp[n];
}
```

Let's take i=8 for example. My code makes j run 4 times
(j=1,2,3,4) but by making 2*j, this code runs also 4 times.
Does this really save time?

to be continued
