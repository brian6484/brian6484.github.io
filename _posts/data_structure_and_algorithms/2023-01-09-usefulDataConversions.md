---
layout: post
title: Useful Java data conversion tricks
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
---
## Character.isDigit()
boolean isDigit(char ch) checks if this character is a digit
```java
while(!queue.isEmpty()){
    char c = queue.poll();
    if(Character.isDigit(c)){
        num = num*10 + c - '0';
    }
```
## check if char 
```java
char c >= '0'
```

## s.charAt(i)-'0'
When converting character (e.g. ‘3’) to integer to use as index in array, have to subtract ASCII value of ‘0’.

## int s = Character.getNumericValue(secret.charAt(i));
This is same as doing s.charAt(i)-'0', getting the int value of char.

## string to set<Character>
```java
Set<Character> set1= "qwertyuiop".chars().mapToObj(c-> (char)c).collect(Collectors.toSet());
```

## converting ArrayList to Array for int[] solution
```java
List<String> result = new ArrayList<>();
result.toArray(new String[result.size()]);
```

Actually, if you have a list and you put all ur elements inside it,
you can create a array of list.size() and do array[i] = list.get(i)
like this 

```java
List<Integer> list = new ArrayList<>();
int[] ans = new int[list.size()];
for(int i=0; i<list.size(); i++){
    ans[i] = list.get(i);
}
return ans;
```

## convert array to ArrayList and add in constructor
```java
Set<Character> set = new HashSet<>(Arrays.asList('a','e','i','o','u','A','E','I','O','U'));
```

## make string from array
```java
char[] arr = s.toCharArray();
//bla bla do with arr
return new String(arr);
```

## stream elements in set to int[] array
[this](https://leetcode.com/problems/intersection-of-two-arrays/)
```java
public int[] intersection(int[] nums1, int[] nums2) {
    Set<Integer> set = new HashSet<>();
    for (int i = 0; i < nums1.length; i++) {
        set.add(nums1[i]);
    }
    Set<Integer> result  = new HashSet<>();
    for(int i=0; i<nums2.length; i++){
        if(set.contains(nums2[i])){
            result.add(nums2[i]);
        }
    }
    return result.stream().mapToInt(k->k).toArray();
```

## convert ascii value to binary
```java
//The reason use 1<< is that let the value of 'a' to be 1?
//Yes, otherwise, 'a' will be missed since 'a' - 'a' = 0.
for(int i=0; i<len; i++){
    for(char c : words[i].toCharArray()){
    value[i] |= 1<<(c-'a');
    }
}
// a 1->1
// b 2->10
// c 4->100
// ab 3->11
// ac 5->101
// abc 7->111
// az 33554433->10000000000000000000000001
```

## pq.addAll()
This method inserts all elements in a collection inside a PQ.
```java
PriorityQueue<Map.Entry<Character,Integer>> pq = new PriorityQueue<>((a,b) ->b.getValue()-a.getValue());
pq.addAll(map.entrySet());
```

And when you poll from PQ, it is type Map.Entry so if you want to
use its Value, you have to cast it back to (int):
```java
StringBuilder sb = new StringBuilder();
while(!pq.isEmpty()){
    Map.Entry e = pq.poll();
    for(int i=0; i< (int) e.getValue();i++){
        sb.append(e.getKey());
    }
    
}
return sb.toString();
```

## declare 2d array right away
```java
int[][] dir = {{0,1},{1,0},{-1,0},{0,-1}};
```

## TreeMap.lowerKey(int key)
It returns the **greatest key** strictly less than the key passed
as parameter.
