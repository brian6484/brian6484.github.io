---
layout: post
title: 2 different ways to create 2D array (List vs ArrayList?)
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
  - Head First Java
---

## First way
```java
List<Integer>[] graph = (ArrayList<Integer>[]) new ArrayList[n];
for (int i = 0; i < n; i++) {
    graph[i] = new ArrayList<>();
}

for (int[] e : edges) {
graph[e[0]].add(e[1]);
graph[e[1]].add(e[0]);
}
```

Notice we cannot use ArrayList method's get() like graph.get(). 
Instead, we manually enter the index via graph[].

## Second way
```java
// List<List<Integer>> list = new ArrayList<>(2);
// for(int i=0; i<2;i++){
//     list.add(new ArrayList());
// }
List<List<Integer>> list = Arrays.asList(new ArrayList<>(), new ArrayList<>());
```

In here, we can indeed use .get() method provided by ArrayList.

I am assuming first way is using Array while second way is using
ArrayList.

