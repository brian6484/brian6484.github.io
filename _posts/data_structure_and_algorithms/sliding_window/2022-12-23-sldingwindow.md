---
layout: post
title: Sliding window
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
  - Sliding window
---
There is a list of sliding window [question list](https://leetcode.com/problems/subarrays-with-k-different-integers/solutions/523136/java-c-python-sliding-window/?orderBy=most_votes)
at the end.

## Explanation
Sliding is commonly used in problems that involve finding a subarray or 
substring that satisfies specific conditions. https://learning-e.tistory.com/36

1) Subarray/Substring Sum Problems: Find a subarray or substring with a 
given sum, sum within a certain range, or the maximum/minimum sum. 

2) Subarray/Substring with a Fixed Length(k): The sliding window approach 
can efficiently traverse the array or string while keeping track of the 
fixed-length window's properties.

3) Longest Substring with Unique Characters: can efficiently handle this by maintaining a set or hashmap of characters within the current window.

4) Two-Pointer Technique: Problems where you need to find a pair of 
elements that satisfy certain conditions. The sliding window approach can 
often be used as a variation of the two-pointer technique by adjusting 
the window boundaries based on the current conditions. **BUT TWO POINTER 
cannot have duplicate values and list should be sorted!!* So if you have
duplicate values, use sliding window.

5) Fixed-Size Window Over a Data Stream: Problems where you need to maintain a fixed-size window over a continuous data stream and update the window's properties efficiently as new data arrives. The sliding window technique can efficiently handle this scenario by adding new elements and removing old elements from the window.


## General approach
Let's say we are solving 1) finding shortest subsequence that has sum equal
to k. If subsequence lengths are the same, sort by the starting index (e.g. 
[0,2] is the answer instead of [1,3])

```python
def solution(sequence, k):
    answer = []
    start,end=0,0
    cur_sum=0
    length=float('inf')
    while end<len(sequence):
        cur_sum+=sequence[end]
        while cur_sum>k:
            cur_sum -= sequence[start]
            start+=1
        if cur_sum==k:
            subseq_length= end-start+1
            if subseq_length<length:
                length=subseq_length
                # if result already had some content, it will be replaced entirely with the new list. 
                answer=[[start,end]]
            elif subseq_length==length:
                answer.append([start,end])
            # if subseq_length<=length:
            #     answer.append(sequence[start:end+1])
            #     length=subseq_length
            
        end+=1
            
    return answer[0]
```

Btw answer =[[start,end]] is important cuz we want to clear our answer list
when we find a subsequence that is shorter than any we have encountered so 
far. 

Explanation:

Start with two pointers, start and end, both initialized to 0, and a variable current_sum initialized to 0. These pointers represent the boundaries of the current subarray being considered, and current_sum will store the sum of elements within the window.

Increment the end pointer until the current sum becomes greater than or equal to the target k. At each step, add the element at index end to the current_sum.

Once the current sum becomes greater than or equal to k, start moving the start pointer to the right while reducing the current_sum. This step is performed in a while loop to ensure the subarray sum remains less than or equal to k.

If the current_sum becomes equal to k, check the length of the current subarray (end - start + 1). If the length is smaller than the minimum length found so far, update the minimum length and store the current subarray as the possible answer. If the length is equal to the minimum length found so far, add the current subarray to the list of possible answers.

Continue the process by incrementing the end pointer and adjusting the start pointer as necessary until the end of the input sequence is reached.

After processing all elements, the result list will contain all subarrays that sum to k and have the shortest length.

By using the sliding window approach, we can efficiently traverse the sequence in linear time and find all subarrays that meet the given conditions. The solution avoids unnecessary computations and makes sure that the output list contains only the shortest subarrays that sum to k.

This is more smooth though
```python
def solution(sequence, k):
    """ 연속된 부분 수열의 합

    sol. 
    누적 합 행렬을 사용하여 구간합을 빠르게 계산할 수 있도록 한다.
    수열은 오름차순으로 정렬되어 있고, 연속된 수열의 합을 계산하기 때문에 
    두 개의 포인터를 사용하여 목표 값 k 를 찾도록 한다

    앞쪽 포인터는 그대로 두고 뒤쪽 포인터를 이동시켜가며 k 값에 가까워지는지 확인한다
    만약 구간 합이 k 보다 작다면 더 큰 수가 필요한 것 이기 때문에 뒤쪽 포인터를 더 뒤로 이동시킨다
    만약 구간 합이 k 보다 크가면 구간 내에서 일정 값을 덜어내야 하기 때문에 작은 값들을 먼저 버리도록 앞쪽 포인터를 뒤로 이동시킨다

    만약 구간 합이 k 인 지점을 찾았다면 정답을 기록한다. 
    이 때 구간합에 사용된 요소 개수가 작은 구간을 선택하도록 한다.


    """
    answer = []
    arr = [sequence[0]]
    for i in range(1, len(sequence)):
        num = sequence[i] + arr[-1]
        arr.append(num)

    start = 0
    end = 0
    answer = None
    answer_idx = None
    cnt = 0
    while start <= end and end < len(sequence):
        s = arr[start]
        e = arr[end]
        val = e - s + sequence[start]
        # print(start, end, val)
        if val == k:
            if answer is None:
                answer = [start, end]
            else:
                if (answer[-1] - answer[0]) > (end - start):
                    answer = [start, end]

        if start == end:
            end += 1
        elif val > k:
            start += 1
        else:
            end += 1

    return answer
```

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
