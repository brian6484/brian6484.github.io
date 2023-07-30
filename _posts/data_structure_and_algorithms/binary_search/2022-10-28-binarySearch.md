---
layout: post
title:  Binary Search explained
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
---

## Binary search original template
  
## start vs start -1
Ok before this lemme explain what start really means in binary search. We
are NOT going to use end pointer cuz it is complicated and start pointer
is sufficient. So firstly, we have the 2 common templates - start<end or
start<=end.

If you start with start<end, when that search ends, at the previous step
start would have been incremented by value 1 (that is the reason why we
exit out of that while loop). Now this start is the minimal value that
satisfies the condition you have set in search. So start is the answer if
you want to find the minimum value. But if you are required to take a step
back and need to return a value before we reach that minimum value, it is
start -1.

It is fine if you don’t get it now. Let me finish explaining start<=end.
Now the difference is that unlike the previous start<end, the loop will
run **one more time**. When we exit this while loop via (end= mid+1) and
notice we are not increasing the value of start but instead shifting the
end pointer, the value start is again the minimum value that satisfies the
condition you have set in search. Now what is start-1? If the question
does not ask for the minimum value but when you need to take a step back
and return a value before we reach that minimum value, we return start-1.
