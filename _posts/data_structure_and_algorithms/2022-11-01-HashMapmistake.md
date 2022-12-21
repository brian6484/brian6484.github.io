---
layout: post
title: Mistake in dealing with HashMap
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
---

## Example
This [example](https://leetcode.com/problems/ransom-note/description/)

My initial solution:
```java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        Map<Character,Integer> map = new HashMap<>();
        for(char c:magazine.toCharArray()){
            map.put(c, map.getOrDefault(c,0)+1);
        }
        for(char c:ransomNote.toCharArray()){
            if(!map.containsKey(c)) return false;
            int value = map.get(c);
            System.out.println(value);
            if(value<=0) return false;
            map.put(c,value--);
        }
        return true;
    }
}
```

I kept getting issue with test case of "aa" and "ab" for ransomNote
and magazine respectively.

BTW hashmap do not allow duplicate keys so we can update the number
of occurrence of the character by putting the updated number again
into the hashmap.

My mistake: I was post-decrementing the "value" so the updated
"value" was not placed. Solution is to change it to pre-decrement.

Better solution:
```java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        Map<Character,Integer> map = new HashMap<>();
        for(char c:magazine.toCharArray()){
            map.put(c, map.getOrDefault(c,0)+1);
        }
        for(char c:ransomNote.toCharArray()){
            int updatedCount = map.getOrDefault(c,0)-1;
            if(updatedCount<0) return false;
            map.put(c,updatedCount);
        }
        return true;
    }
}
```
