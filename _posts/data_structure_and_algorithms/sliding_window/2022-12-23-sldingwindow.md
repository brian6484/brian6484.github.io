---
layout: post
title: Sliding window
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
---
There is a list of sliding window [question list](https://leetcode.com/problems/subarrays-with-k-different-integers/solutions/523136/java-c-python-sliding-window/?orderBy=most_votes)
at the end.

## Leetcode 1358. Number of Substrings Containing All Three Characters
### Solution 1
We mark the count of a,b and c as we move our right pointer
to the right. When and while all the counts are greater than 1, we move
our left pointer to the right and decrement the counter of
character that left pointer passes.

Very important, why we do res += left is because we can create
substrings with however many characters we passed with our 
left pointer.

For example, "aaabbcca", when right pointer is at index 5,
all counters are greater than 0. We move left pointer to index
3 after the while loop finishes executing. We add 3 to the answer
because we can create 3 substrings with the 3 characters passed
by our left pointer. (abbc, aabbc, aaabbc).

Then a,b,c > 0 at right = 7 ,then we will move i until i = 5 
then we will add 5 to result because there could be 5 
substrings starting from 0 to second b.

```java
public int numberOfSubstrings(String s) {
    int[] count = {0,0,0};
    int ans=0;
    int left =0;
    for(int right=0;right<s.length(); right++){
        count[s.charAt(right)-'a']++;
        while(count[0]>0 && count[1]>0 && count[2]>0){
            count[s.charAt(left++)-'a']--;
        }
        ans += left;
    }
    return ans;
}
```

### Solution 2
This time, count will mark the index of the character last found.
If the ending index of substring is i, starting position index
should be at min(count) to have all 3 characters. For substring,
starting index can start from [0, min(last)] so min(last) +1.

```java
public int numberOfSubstrings(String s) {
    int[] count = {-1,-1,-1};
    int ans=0;
    for(int i=0; i<s.length();i++){
        count[s.charAt(i)-'a'] =i;
        ans += 1+ Math.min(count[0],Math.min(count[1],count[2]));
    }
    return ans;
}
```

## Leetcode 2063. Vowels of All Substrings
### Solution 1
If there is a vowel somewhere in a string, for that each vowel
s[i], it can be in a substring that starts at s[x] and ends at
s[y], where 0 <= x <= i and i <= y < n. So for x, we have i+1
choices and n-i for y.

Thus, there are (i+1)*(n-i) substrings containing s[i] vowel.

```java
public long countVowels(String s) {
    long res = 0, n = s.length();
    for (int i = 0; i < n; i++)
        if ("aeiou".indexOf(s.charAt(i)) >= 0)
            res += (i + 1) * (n - i);
    return res;
}
```

### Solution 2
More brute-force approach.

I don't get it tbc

```java
public long countVowels(String word) {
    long res = 0, prev = 0;
    for(int i=0; i<word.length(); i++) {
        char c = word.charAt(i);
        if(c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u')
            prev += i + 1;
        res += prev;
    }
    
    return res;
}
```

## Leetcode 209. Minimum Size Subarray Sum
### Solution  with 2 pointer
Eassy but if confused sometimes, my youtube video will help
```java
public int minSubArrayLen(int target, int[] nums) {
    int len = nums.length;
    int sum=0, from =0, minLength= Integer.MAX_VALUE;
    for(int i=0; i<len; i++){
        sum += nums[i];
        while(sum>=target){
            minLength = Math.min(minLength, i-from+1);
            sum -= nums[from++];
        }
    }
    return minLength==Integer.MAX_VALUE ? 0:minLength;
}
```

## 
