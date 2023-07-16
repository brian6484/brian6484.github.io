---
layout: post
title: Floyd Warshall algorithm
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
---

## Floyd Warshall algorithm
Floyd Warshall is used not only in finding shortest path between **all edges**
but we can also use it to find *transitive closure*. Transitive closure of
a directed graph represents basically the reachability between every pair of
nodes in graph. Like from node a is it possible to reach till node m through
paths.

For example, if i->k is False and k->j is False, then we know i->j is also
False. So when calculating, matrix[i][j] will be made False. But it is important
to think in the opposite direction too. matrix[j][i] will be True on the
other hand.

chatgpt:
The Floyd-Warshall algorithm is a graph algorithm used to find the shortest path between all pairs of nodes in a weighted graph. It can handle both positive and negative edge weights, but it does not handle negative cycles.

The algorithm works by iteratively considering all possible intermediate nodes and updating the distances between pairs of nodes. It constructs a distance matrix that represents the shortest distances between every pair of nodes in the graph.

The main use of the Floyd-Warshall algorithm is to solve the All-Pairs Shortest Path problem, where you need to find the shortest path between every pair of nodes in a graph. It is especially useful when you have a dense graph (lots of edges) and need to find the shortest paths between all pairs of nodes.

The algorithm has a time complexity of O(V^3), where V is the number of nodes in the graph. This makes it efficient for small to medium-sized graphs but can become computationally expensive for large graphs.

In the context of the given problem, we can use the Floyd-Warshall algorithm to find the transitive closure of the graph, which helps determine the accurate rankings of the players based on the game results. By considering all possible paths between pairs of players, the algorithm helps identify players who can be reached from each other in terms of winning games.


## Practice question
### 순위
https://school.programmers.co.kr/learn/courses/30/lessons/49191

Floyd-Warshall can be used to find transitive closure. So For example, 
if i->k is False  and k->j is False, then we know i->j is also
False. So when calculating, matrix[i][j] will be made False. But it is important
to think in the opposite direction too. matrix[j][i] will be True on the
other hand.

Thus the code should be 
```python
from math import inf
def solution(n, results):
  graph = [[inf for _ in range(n+1)] for _ in range(n+1)]
  for i in range(1,n+1):
    graph[i][i]=0
  for winner,loser in results:
    graph[winner][loser]=1
    graph[loser][winner]=-1
  for k in range(1,n+1):
    for i in range(1,n+1):
      for j in range(1,n+1):
        if graph[i][k]==1 and graph[k][j]==1:
          graph[i][j]=1
          graph[k][i]=graph[j][k]=graph[j][i]=-1
        # graph[i][j]=min(graph[i][j], graph[i][k]+graph[k][j])
  # print(graph)
  count = 0
  
  for row in graph:
      if row.count(inf) == 1:
          count += 1  
  print(count)
  return count
```

A better solution:
```python
def solution(n, results):
    answer = 0
    win_graph = defaultdict(set)    # 이긴 애들
    lose_graph = defaultdict(set)   # 진 애들
    
    for winner,loser in results:        # 결과에서 이기고 진 애들 그래프화
        win_graph[loser].add(winner)
        lose_graph[winner].add(loser)

    for i in range(1,n+1):         
        for winner in win_graph[i]:                    # i한테 진 애들은 i를 이긴 애들한테도 진 것
            lose_graph[winner].update(lose_graph[i])
        for loser in lose_graph[i]:                     # i한테 이긴 애들은 i한테 진 애들한테도 이긴 것
            win_graph[loser].update(win_graph[i])
    
    for i in range(1,n+1):
        if len(win_graph[i]) + len(lose_graph[i]) == n-1:   # i한테 이기고 진 애들 합쳐서 n-1이면 순위가 결정된 것
            answer += 1

    return answer
```


