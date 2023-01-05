---
layout: post
title: Bucket sort
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
---
## Issue
While I was solving [this](https://leetcode.com/problems/top-k-frequent-elements/),
I came across the need to somehow solve this in linear time.
The question requires sorting the map's value, which stores
the frequency of that integer.

This [reference explanation](https://leetcode.com/problems/top-k-frequent-elements/solutions/1927648/one-of-the-best-explanation/?orderBy=most_votes)
explained really well.

## Without bucket sort (using PQ)
```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> map = new HashMap<>();
        
        for(int i : nums){
            map.put(i, map.getOrDefault(i, 0) + 1);
        }
        
        PriorityQueue<Integer> maxHeap = new PriorityQueue<>((a,b) -> map.get(b) - map.get(a));
        
        for(int key : map.keySet()){
            maxHeap.add(key);
        }
        
        int res[] = new int[k];
        for(int i = 0; i < k; i++){
            res[i] = maxHeap.poll();
        }
        return res;
    }
}
```

This is O(n log n) time, we can do linear time with bucket sort.

## Bucket sort
Again, look at the reference explanation.
