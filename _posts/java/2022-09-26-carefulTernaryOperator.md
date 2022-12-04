---
layout: post
title: Careful with ternary operator
category: Java
tags:
  - Java
  - Head First Java
---
## Issue
I was doing some Leetcode when I had Compile error regarding some
arithmetic errors.
```yaml
java.lang.ArithmeticException: / by zero
```

My code: 
```java
//long a = leftSum / (i + 1);
//long b = length-i==1 ? 0 : rightSum / (length-(i+1));
long diff = Math.abs(leftSum / (i + 1) - length-i==1 ? 0 : rightSum / (length-(i+1)));
if(diff<min){
    min = diff;
    res = i;
}
```

It worked just fine when I just did Math.abs (a-b) by inputting pre-calculated
values inside Math.abs function. But when I tried saving some space by
ridding a & b and putting all inside my diff variable, this error occurred.

## Solution
You need a bracket to enclose the entire ternary operator as such:
```java
- (length-i==1 ? 0 : rightSum / (length-(i+1)))
```

