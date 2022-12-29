---
layout: post
title: Comparator VS Lambda
category: Java
tags:
  - Java
---
## Issue
There is the problem of [overflow with Lambda](https://brian6484.github.io/java/2022/09/22/overflowLambda.html)
as discussed in my last post. Whilst lambda should be 
avoided in interviews, it can serve a simple sorting
purpose than Comparator. But let's see the difference
in implementing those 2.

## Comparator
For example, in this [leetcode](https://leetcode.com/problems/largest-number/)
we are sorting the strings in string array.

BTW, if s1="9" and s2="31", case1= s1+s2= "931", 
case2= s2+s1 = "319". case1 has a higher value than
case 2 apparently. So we should put s1 in front of s2 
to get higher value.

```java
		// Comparator to decide which string should come first in concatenation
		Comparator<String> comp = new Comparator<String>(){
		    @Override
		    public int compare(String str1, String str2){
		        String s1 = str1 + str2;
				String s2 = str2 + str1;
				return s2.compareTo(s1); // reverse order here, so we can do append() later
		    }
	     };
```

When implementing Comparator, you have to override its
compare() method.

## Lambda
Actually lambda and comparator is kind of same. We use
both compareTo method and since we want a descending order,
it is case2 - case1, not case1 - case2.

```java
//lower value.compareTo(higher value)
Arrays.sort( s_num, (s1, s2) -> (s2+s1).compareTo(s1+s2) );
```



