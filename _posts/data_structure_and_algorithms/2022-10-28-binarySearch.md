---
layout: post
title:  Binary Search
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
---

## Binary search original template
```java
public int search(int[] nums, int target) {
    int left = 0, right = nums.length-1;
    while(left<=right){
        int mid = left +(right-left)/2;
        if(nums[mid]==target) return mid;
        else if (nums[mid]>target) right = mid-1;
        else left = mid+1;
    }
    return -1;
}
```

BTW, **very important**. Since we declared right as arr.length-1,
right is the correct 0-indexed index. So we have to do while condition
until <= right (including the index itself), not < right.

I always wondered, what is the difference between doing right = mid
or right =mid -1? When do we differentiate?

