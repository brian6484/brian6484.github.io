---
layout: post
title: return new String(array) when you modified array
category: Java
tags:
  - Java


---

## Precautions
If you modified string to a char array, and you want to return
   the modified char array, do **return new String(array)**, not just
   *return s*. Technically s is not modified - it is the char array
   that is changed.

This [example](https://leetcode.com/problems/reverse-vowels-of-a-string/solutions/81326/simple-java-solution-one-line-hashset-init/)
```java
public class Solution {
    public String reverseVowels(String s) {
        Set<Character> set = new HashSet<>(Arrays.asList('a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'));
        char[] arr = s.toCharArray();
        int left = 0, right = arr.length - 1;
        while (left < right) {
            if (!set.contains(arr[left])) {
                left++;
            } else if (!set.contains(arr[right])) {
                right--;
            } else {
                char tmp = arr[left];
                arr[left] = arr[right];
                arr[right] = tmp;
                left++;
                right--;
            }
        }
        return new String(arr);
    }
}
```

I tried return s but it does not return the modified string (obviously).
You have to return a new String that takes the char array of string.
