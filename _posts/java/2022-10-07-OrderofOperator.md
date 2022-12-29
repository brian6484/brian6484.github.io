---
layout: post
title: Order of operator in Java (e.g. order matters in &&)
category: Java
tags:
  - Java
  - Head First Java
---
## Reference
https://park-youjin.tistory.com/11

This reference lists order of all operators in Java. Let's
look at the and (&&) operator in particular in this Leetcode
[problem](https://leetcode.com/problems/battleships-in-a-board/description/)

## Order in &&
Notice this code solution
```java
class Solution {
    public int countBattleships(char[][] board) {
        int m = board.length;
        if(m==0) return 0;
        int n = board[0].length;

        int count = 0;
        for(int i=0; i<board.length; i++){
            for(int j=0;j<board[0].length;j++){
                if(board[i][j]=='.') continue;
                if(i>0 && board[i-1][j]=='X') continue;
                if(j>0 && board[i][j-1]=='X') continue;
                count++;
            }
        }
        return count;
    }
}
```

As you see, order in && operator is from left to right. This
means the condition on the left will be checked first. So
the more important condition of i>0 should come first.

I tried doing board[][] && i>0 but I get this error:
```yaml
ArrayIndexOutOfBoundsException: Index -1 out of bounds for length 3
```

So we can see i>0 condition is not being checked here.
