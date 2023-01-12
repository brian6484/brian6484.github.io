---
layout: post
title: General approach to backtracking + template
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
---

I was solving [palindrome partitioning](https://leetcode.com/problems/palindrome-partitioning/solutions/182307/java-backtracking-template-general-approach/?orderBy=most_votes)
when I decided to compile some notes for backtracking.

## Backtracking 
There are 3 main steps in backtracking - choose, explore, unchoose.

For this problem:
1) we choose each substring
2) we explore the remaining substring 
3) do opposite operation of choose

Normally, we make a helper() function to accept more parameters.

For parameters in our function, we need:

1. The object you are working on:  For this problem is String s.
2. A start index or an end index which indicate which part you are working on: For this problem, we use substring to indicate the start index.
3. A step result, to remember current choose and then do unchoose : For this problem, we use List<String> step.
4. A final result, to remember the final result. Usually when we add, we use 'result.add(new ArrayList<>(step))' instead of 'result.add(step)', since step is reference passed. We will modify step later, so we need to copy it and add the copy to the result;

Base case: The base case defines when to add step into result, and when to return.

Choose : In this problem, if the substring of s is palindrome, we add it into the step, which means we choose this substring.

Explore : In this problem, we want to do the same thing to the remaining substring. So we recursively call our function.

Un-Choose : We draw back, remove the chosen substring, in order to try other options.

## Visual diagram

<img src="/assets/images/posts/data_structure_and_algorithm/Backtracking/2Qx2ZBx.jpg" title="제목" alt="아무거나" width="400"/> 

<img src="/assets/images/posts/data_structure_and_algorithm/Backtracking/backtracking.png" title="제목" alt="아무거나" width="400"/>

## Templates
https://leetcode.com/problems/subsets/solutions/27281/A-general-approach-to-backtracking-questions-in-Java-(Subsets-Permutations-Combination-Sum-Palindrome-Partitioning)/

