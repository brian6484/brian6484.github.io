---
layout: post
title: Dictionary useful methods and practice questions
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
---
  
## Dictionary
### Counter 
Counter is a subclass of dictionary and thus has all methods of dictionary.
We can actually compare Counter object with dictionary with == 

```python
for i in range(len(discount)-9):
    if dic == Counter(discount[i:i+10]): 
        answer += 1
```

And Counter is a dictionary-like object, which means it looks something like
```python
Counter({'mislav': 1})
```
So if you want to get its key or value, you probably want to convert it to a
list using *list()* because if you just do counter.keys(), you get
```python
dict_keys(['vinko'])
```

So convert it to a list like
```python
answer = list(count.keys())

# if you want to get first key in the list of keys only, 
# this is same as list[0]
# answer = list(count.keys())[0]
```

If you want to get a specific index as the key like [["yellow_hat", "headgear"], ["blue_sunglasses", "eyewear"], ["green_turban", "headgear"]]
and you want a Counter with keys on the second index,

Either way is fine
```python
count = Counter(cloth[1] for cloth in clothes)
print(count)
cnt = Counter([kind for name, kind in clothes])
print(cnt)

# Counter({'headgear': 2, 'eyewear': 1})
```



### dict.keySet() = dict.items()
Java Dictionary's keySet(), which consists of both key and value, is
same as .items()
```python
for key,value in dict.items():
  
# Set<String> keySet = map.keySet();
# for (String key : keySet) {
#   System.out.println(key);
# }
```

### dict.contains(key) = if key in dict
Checking if dict contains this key can be done via
```python
if key in dict:
if key not in dict:

# if dict.contains(key):
```

### dic.get(key,0)
This is same as Java where if there is no such key found, we initialise
that value for that key as 0. If we don't do this and conduct some logic
on our dic's key right away like
```python
dic={}
for i in nums:
    dic[i]+=1
```

We will get a *KeyError* because there is no such key stored in our dict yet.

### dic = defaultdict(list)
To avoid KeyError and if our dictionary needs to hold a list as a value,
we can initialise this easily via

```python
dic = defaultdict(list)
```

### dict[key] = set()
If you want to set a set for a specific key so that no duplicate values
are allowed for that key, declare it like this
```python
dict[key] = set()
dict[key].add("hi")


# Map<String, Set<Integer>> map = new HashMap<>();
# map.put("key1", new HashSet<>());
# map.put("key2", new HashSet<>());
```

### iterating through highest keys in descending order
You can iterate through the highest keys in a dictionary by using the 
`sorted()` function with the `keys()` method of the dictionary.

```python
my_dict = {'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5}

# Get the highest keys in descending order
highest_keys = sorted(my_dict.keys(), reverse=True)

# Iterate through the highest keys
for key in highest_keys:
    value = my_dict[key]
    print(key, value)
```

Output:
```
e 5
d 4
c 3
b 2
a 1
```

So you are effectively not sorting the dictionary itself, but smartly 
sorting the keys in descending order **in a list** separately and 
passing that key to dict to get the value.

### sorted() with dictionary's key and value
If we want to sort either dict's key or value or both (.items()), we 
need to use **sorted()** first. Then, we pass what we want to sort (key,
value, item) and a lambda function where we set the key parameter condition for sorting.
If we want to sort based on the second index, we do 
```python
key = lambda x :x[1]
```

Also, very important that the sorted() produces a completely different list
from the original list. We **do not** modify the original list so we have
to declare another variable to get that new sorted list like
```python
list = [3,2,4]
this_is_the_sorted_list = sorted(list)
```

If we don't, there is no point because we didnt modify the list in the end.
If you want to the original list to be modified, use sort() instead
```python
citations.sort(reverse=True)
```

Anyway, For 베스트앨범, we first get the key and value from dicCount where
value is in descending order, and we use that key from dicCount and pass
that into the inner for loop, where we get dicOrder[key], which contains
a tuple of (index,value). We sort here on the value here too so x[1] for
key lambda. Lastly, we slice that new sorted list via [:2], which means we only
get 0th and 1st element in that new list.

```python
dicOrder= defaultdict(list)
dicCount = {}
for key,totalCount in sorted(dicCount.items(),key= lambda x: x[1],reverse=True):
    for index,value in sorted(dicOrder[key], key=lambda x:x[1],reverse=True)[:2]:
```


## Practice questions
### 완주하지 못한 선수
https://school.programmers.co.kr/learn/courses/30/lessons/42576

Important that if you want to use Counter's key or object, we need to 
convert its key or value into a list via **list()**

```python
from collections import Counter

def solution(participant, completion):

  count = (Counter(participant)-Counter(completion))
  answer = list(count.keys())[0]
  return answer
```

### 폰켓몬
https://school.programmers.co.kr/learn/courses/30/lessons/1845

Note that to avoid KeyError, we need to put default value for a key that
does not exist in our dict yet. That can be done via .get(key,0)

```python
def solution(nums):
    print(set(nums))
    dic={}
    for i in nums:
        dic[i]=dic.get(i,0)+1
    length = len(dic)
    return len(nums)//2 if length>len(nums)//2 else length
```

### 의상
https://school.programmers.co.kr/learn/courses/30/lessons/42578

V important is that If you want to get a specific index as the key,
do it like count or cnt. Either way is fine. 
```python
from collections import Counter
from functools import reduce

def solution(clothes):
    count = Counter(cloth[1] for cloth in clothes)
    print(count)
    cnt = Counter([kind for name, kind in clothes])
    print(cnt)
    value = list(count.values())
    product = reduce(lambda x,y: (x+1)*(y+1)-1, value)
    
    return product
```

Then, we consider the possbilities of each clothes. We can either wear
A,B or none so if we have 2 types of hat, we have 3 (2+1) possibilities.
We multiply the possibilies but **minus one** because we cannot have the
possibility of not wearing anything.

I got the explanation here
https://coding-grandpa.tistory.com/88

### 베스트앨범 (Hard)
https://school.programmers.co.kr/learn/courses/30/lessons/42579

Anyway, For 베스트앨범, we first get the key and value from dicCount where
value is in descending order, and we use that key from dicCount and pass
that into the inner for loop, where we get dicOrder[key], which contains
a tuple of (index,value). We sort here on the value here too so x[1] for
key lambda. Lastly, we slice that new sorted list via [:2], which means we only
get 0th and 1st element in that new list.
```python
from collections import defaultdict
def solution(genres, plays):
    dicOrder= defaultdict(list)
    dicCount = {}
    answer = []
    index = 0
    for key,value in zip(genres,plays):
        dicOrder[key].append((index,value))
        dicCount[key] = dicCount.get(key,0)+value
        index+=1
    for key,totalCount in sorted(dicCount.items(),key= lambda x: x[1],reverse=True):
        for index,value in sorted(dicOrder[key], key=lambda x:x[1],reverse=True)[:2]:
            answer.append(index)
    return answer
```

We can further optimise via using enumerate on top of zip to get the
index like
```python
    for index, (key,value) in enumerate(zip(genres,plays)):
        dicOrder[key].append((index,value))
        dicCount[key] = dicCount.get(key,0)+value
```
