---
layout: post
title: Use Deque over Stack in Java!
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
---
## Explanation
This [reference](https://stackoverflow.com/questions/12524826/why-should-i-use-deque-over-stack)
explains why deque should always be chosen over stack.

Stack extends Vector class, which is an old, deprecated class.

Just use deque, I think its methods are more intuitive too.

## Difference in methods
Let's take [this](https://leetcode.com/problems/remove-k-digits/description/)
as example. It can be solved via both stack and deque.

Stack:
```java
class Solution {
    public String removeKdigits(String num, int k) {
        StringBuilder sb = new StringBuilder();
        Stack<Character> stack = new Stack<>();
        if(k==num.length())        
            return "0";
        int i = 0;
        while(i<num.length()){
            while(k>0 && !stack.isEmpty() && stack.peek()>num.charAt(i)){
                stack.pop();
                k--;
            }
            stack.push(num.charAt(i));
            i++;
        }

        while(k>0){
            stack.pop();
            k--;            
        }

        while(!stack.isEmpty()){
            sb.append(stack.pop());
        }
        
        while(sb.length()>1 && sb.charAt(sb.length()-1)=='0'){
            sb.deleteCharAt(sb.length()-1);
        }

        return sb.reverse().toString();


    }
}
```

Deque:
```java
class Solution {
    public String removeKdigits(String num, int k) {        
        if(k >= num.length()) return "0";

        Deque<Character> stack = new ArrayDeque<>();
        for(char c : num.toCharArray()) {
            while(k > 0 && !stack.isEmpty() && stack.peekLast() > c) {
                stack.removeLast();
                k--;
            }
            stack.addLast(c);
        }
        
        while(k>0) {
            stack.removeLast();
            k--;
        }
        
        // Remove all zeros from the front of the stack and then if stack is empty, return "0"
        while(!stack.isEmpty() && stack.peekFirst()== '0') stack.removeFirst();
        if(stack.isEmpty()) return "0";

        // build the number from the stack
        StringBuilder sb = new StringBuilder();
        while(!stack.isEmpty()) {
            sb.append(stack.removeFirst());
        }
        return sb.toString();
    }
}
```
