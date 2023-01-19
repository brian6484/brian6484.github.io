---
layout: post
title: Deducing ternary operator in Java
category: Java
tags:
  - Java
  - Head First Java
---
## Deduction
I was solving maximum subarray [question](https://leetcode.com/problems/maximum-subarray/description/)
when I found a useful explanation to break down and deduce
ternary operator.

```java
public int maxSubArray(int[] nums) {
    int n = nums.length;
    int[] dp = new int[n];
    dp[0] = nums[0];
    int max = dp[0];
    for(int i=1;i<nums.length;i++){
        //this is deduction of ternary operator
        // dp[i] = Math.max(nums[i]+dp[i-1], nums[i]);
        // dp[i] = nums[i] + Math.max(dp[i-1],0)
        dp[i] = nums[i] + (dp[i-1]>0 ? dp[i-1] : 0);
        max = Math.max(max,dp[i]);
    }
    return max;
}
```

The first commented runs just fine but this ternary operator
looks much cleaner.
