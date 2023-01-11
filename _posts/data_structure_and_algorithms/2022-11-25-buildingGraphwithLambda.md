---
layout: post
title: How to build graph with lambda? 
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
---

## Approach
I was solving this to build a graph, given some edges. [here](https://leetcode.com/problems/minimum-time-to-collect-all-apples-in-a-tree/)

Without lambda, for each edge, we create a temporary list and add
the edges both ways (e.g. [0,1] and [1,0]). Then, we add that
list to our HashMap called graph, the key being the starting
and ending point of edge.

```java
private Map<Integer, List<Integer>> createGraph(int[][] edges) {
    Map<Integer, List<Integer>> graph = new HashMap<>();
  
    for(int i = 0; i < edges.length; i++) {
        List<Integer> list = graph.getOrDefault(edges[i][0], new ArrayList<>()); // Adjecency list representation.
        list.add(edges[i][1]);
        graph.put(edges[i][0], list);
  
  list = graph.getOrDefault(edges[i][1], new ArrayList<>()); // Adjecency list representation.
        list.add(edges[i][0]);
        graph.put(edges[i][1], list);
    }
  
    return graph;
}
```

With lambda:

btw hashmap.computeIfAbsent is similar to .getOrDefault. It computes
some logic you placed in the 2nd parameter if the key passed
as 1st parameter is null.
```java
Map<Integer, List<Integer>> graph = new HashMap<>();
for (int[] edge : edges) {
    graph.computeIfAbsent(edge[0], k -> new ArrayList<>()).add(edge[1]);
    graph.computeIfAbsent(edge[1], k -> new ArrayList<>()).add(edge[0]);
}
```





