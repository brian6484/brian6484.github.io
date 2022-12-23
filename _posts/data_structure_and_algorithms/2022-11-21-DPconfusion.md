---
layout: post
title: Dynamic Programming error
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
---

## Approach
This [example](https://leetcode.com/problems/triangle/description/)

my solution:
```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        int row = triangle.size();
        int col = triangle.get(row-1).size();
        int[] dp = new int[col];
        dp[0] = triangle.get(0).get(0);

        for(int i=1; i<row;i++){
            List<Integer> cur = triangle.get(i);
            for(int j=0; j<cur.size; j++){
//            correct ans is below
//            for(int j = cur.size() - 1; j >= 0; j--){
                if(j==0){
                    dp[0] = dp[0] + cur.get(j);
                }
                else if(j==cur.size()-1){
                    dp[j] = dp[j-1] +cur.get(j); 
                }
                else{
                    dp[j] = Math.min(dp[j-1],dp[j]) + cur.get(j);
                }
            }
        }
        int min = Integer.MAX_VALUE;
        for(int a:dp){
            min = Math.min(min,a);
        }
        return min;
    }
}
```

Why is mine wrong?

Btw bottom-top approach is better here
```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        // corner case
        if(triangle == null || triangle.size() == 0) return 0;
        
        // M[i] represents the min total from bottom to current position
        // copy the last row in triangle to M
        int m = triangle.size();
        int n = triangle.get(m - 1).size();
        int[] M = new int[n];
        for(int i = 0; i < n; i++){
            M[i] = triangle.get(m - 1).get(i);
        }
        
        // induction rule
        // M[i] = min(M[i], M[i + 1]) + curVal
        for(int i = n - 2; i >= 0; i--){
            List<Integer> cur = triangle.get(i);
            for(int j = 0; j < cur.size(); j++){
                M[j] = Math.min(M[j], M[j + 1]) + cur.get(j);
            }
        }
        
        return M[0]; 
    }
}
```

