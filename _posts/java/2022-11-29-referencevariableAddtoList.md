---
layout: post
title: How does reference variable work when adding it to list
category: Java
tags:
  - Java
  - Head First Java
---
## Issue
I was solving this [leetcode](https://leetcode.com/problems/merge-intervals/description/)
when I was baffled by the solution. 

```java
class Solution {
    public int[][] merge(int[][] intervals) {
        Arrays.sort(intervals, (a,b)->Integer.compare(a[0],b[0]));
        int[] newInterval = intervals[0];
        List<int[]> list = new ArrayList<>();
        list.add(newInterval);
        for(int[] interval:intervals){
            if(newInterval[1]>=interval[0]){
                //newInterval values can be changed because we add a "reference variable" newInterval to the list
                //so if it is changed, it is updated in the list
                newInterval[1] = Math.max(newInterval[1],interval[1]); 
            }
            else{
                newInterval = interval;
                list.add(newInterval);
            }
        }
        return list.toArray(new int[list.size()][]);
    }
}
```

The solution added
an integer array to the list first, then changed some values
of that array then the list had that updated array inside it.
How does that work?

## Explanation
What we added to our list is not the actual array object itself,
but the reference to it. So when the object is altered,
since list has the reference to that object, it gets the updated
object reference. 

But once we change that reference to that object in that else
statement, we drop the reference to the old object and link it
with a new one. So the old object is "finalised" inside the
list.
