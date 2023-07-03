---
layout: post
title: Quick union (not quick find)
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
---
## Concept
[This](https://kistone.tistory.com/58) explains well
This [virtual explanation](https://m.blog.naver.com/parkhj2416/221861837543)
too

https://techblog-history-younghunjo1.tistory.com/257 Python version

## Template
```python
def find_parent(parent,x):
    if parent[x]!=x:
        # path compression
        parent[x] = find_parent(parent,parent[x])
      
    #   without path compression
        return find_parent(parent, parent[x])
    return parent[x]

def union(parent,a,b):
    a = find_parent(parent,a)
    b = find_parent(parent,b)
    parent[a] = b
```

```java
public class Union_Find {

    public static int[] parent = new int[1000001];
  
    public static int find(int x) {
      if (x == parent[x])
        return x;
      else
        return parent[x] = find(parent[x]);
    }
  
    public static void union(int x, int y) {
      x = find(x);
      y = find(y);
      // 같은 부모를 가지고 있지 않을 때
      if (x != y) {
        // y가 x 보다 크다는 것을 가정한다면 아래와 같이 표현
        parent[y] = x;
        // 더 작은 값으로 넣어 줄 때 다음과 같이도 표현 가능
        /*
         * if(x < y) parent[y] = x; else parent[x] = y;
         */
      }
    }
  
    // 같은 부모 노드를 가지는지 확인
    public static boolean isSameParent(int x, int y) {
      x = find(x);
      y = find(y);
      if (x == y)
        return true;
      else
        return false;
    }
  
    public static void main(String[] args) {
      for (int i = 1; i <= 8; i++) {
        parent[i] = i;
      }
      union(1, 2);
      union(2, 3);
      System.out.println("1과 3은 연결되어 있나요? " + isSameParent(1, 3));
  
    }

}
```

Leetcode's template is:
```java
class UnionFind {
    private int[] root;

    public UnionFind(int size) {
        root = new int[size];
        for (int i = 0; i < size; i++) {
            root[i] = i;
        }
    }

    public int find(int x) {
        while (x != root[x]) {
            x = root[x];
        }
        return x;
    }

    public void union(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);
        if (rootX != rootY) {
            root[rootY] = rootX;
        }
    }

    public boolean connected(int x, int y) {
        return find(x) == find(y);
    }
}
```


## Example
Let's take this [example](https://leetcode.com/problems/find-if-path-exists-in-graph/description/)
First to understand reason to use union rank, let's explore
DFS and BFS solutions first

### DFS
```java
class Solution {
    private boolean seen;
    public boolean validPath(int n, int[][] edges, int start, int end) {
        boolean[] visited = new boolean[n];
        HashSet<Integer>[] graph = new HashSet[n];

        for(int i=0; i<n; i++){
            graph[i] = new HashSet<Integer>();
        }

        for(int[] edge:edges){
            graph[edge[0]].add(edge[1]);
            graph[edge[1]].add(edge[0]);
        }
        if(graph[start].contains(end)){
            return true;
        }
        seen = false;
        dfs(graph,visited,start,end);
        return seen;
    }

    private void dfs(HashSet<Integer>[] graph, boolean[] visited, int start, int end){
        if(!visited[start]&& !seen){
            if(start==end){
                seen=true;
                return;
            }
            visited[start] = true;
            for(Integer neighbour: graph[start]){
                dfs(graph,visited,neighbour,end);
            }
        }
    }
}
```

### BFS
```java
class Solution {
    public boolean validPath(int n, int[][] edges, int start, int end) {
        boolean[] visited = new boolean[n];
        HashSet<Integer>[] graph = new HashSet[n];
        int i, j;
        
        for(i = 0; i < n; i++){
            graph[i] = new HashSet<Integer>();
        }
        
        for(int[] edge : edges){
            graph[edge[0]].add(edge[1]);
            graph[edge[1]].add(edge[0]);
        }
		
        if(graph[start].contains(end)){  // direct connection exists
            return true;
        }

        Queue<Integer> queue=new LinkedList<>();
        queue.offer(start);
        visited[start] = true;

        while(!queue.isEmpty()){
            int a = queue.size();
            int current = queue.poll();
            if(current ==end) return true;
            for(Integer neighbour:graph[current]){
                if(!visited[neighbour]){
                    visited[neighbour] = true;
                    queue.offer(neighbour);
                }
            }
        }
        return false;
    }
}
```

### Union Find
```java
class DisjointSetUnion{
    private int[] parent;
    private int N;
    public DisjointSetUnion(int n){
        this.N = n;
        this.parent = new int[this.N];
        for(int i=0; i<this.N; i++){
            this.parent[i] = i;
        }
    }
     public boolean areConnected(int u, int v){
         return find(u)==find(v);
     }
     public void union(int u, int v){
         if(u!=v){
             int a = find(u);
             int b = find(v);
             parent[a]=b;
         }
     }
     private int find(int u){
         if(parent[u]==u){
             return u;
         }
         else return parent[u] = find(parent[u]);
     }

}

class Solution {
    public boolean validPath(int n, int[][] edges, int start, int end) {
        DisjointSetUnion set = new DisjointSetUnion(n);
        for(int[] edge : edges){
            set.union(edge[0], edge[1]);
        }
        
        return set.areConnected(start, end);
    }
}
```
