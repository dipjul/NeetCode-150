# [323. Number of Connected Components in an Undirected Graph](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/)
Medium


Given n nodes labeled from 0 to n - 1 and a list of undirected edges (each edge is a pair of nodes), write a function to find the number of connected components in an undirected graph.

Example 1:
```
Input: n = 5 and edges = [[0, 1], [1, 2], [3, 4]]

     0          3
     |          |
     1 --- 2    4 

Output: 2
```
Example 2:
```
Input: n = 5 and edges = [[0, 1], [1, 2], [2, 3], [3, 4]]

     0           4
     |           |
     1 --- 2 --- 3

Output: 1
```
Note: You can assume that no duplicate edges will appear in edges. Since all edges are undirected, [0, 1] is the same as [1, 0] and thus will not appear together in edges.

## Approach
```
1. DFS
  - Number of times dfs called is equal to the number of components
2. Union Find
  - Take number of nodes as the number of components initially
  - if the nodes of an edge are not already connected then decrease the count and union the nodes
```

## Solution
```java
// 1. DFS
class Solution {
  public int countComponents(int n, int[][] edges) {
        HashMap<Integer, List<Integer>> graph = new HashMap<Integer, List<Integer>>();
        boolean[] visited = new boolean[n];

        int count = 0;
        // Step - 1 Build the graph
        for(int i = 0; i < n; i++) {
            graph.put(i, new ArrayList<Integer>());
        }

        for (int i = 0; i < edges.length; i++){
            // Make Undirected Graph
            graph.get(edges[i][0]).add(edges[i][1]);
            graph.get(edges[i][1]).add(edges[i][0]);
        }

        // Step -2 run algorithm
        for (int i = 0; i < n; i++) {
            if(!visited[i]) {
                count++;
                dfs(i, graph, visited);
            }
        }
        return count;

    }

    private void dfs(int at, HashMap<Integer, List<Integer>> graph, boolean[] visited) {
        visited[at] = true;
        for(Integer child: graph.get(at)) {
            if(!visited[child]) {
                dfs(child, graph, visited);
            }
        }
    } 
}

```
```java
// 2. Union Find
class Solution {
    public int countComponents(int n, int[][] edges) {
        UnionFind uf = new UnionFind(n);
        int count = n;
        for(int[] edge: edges) {
            if(uf.isConnected(edge[0], edge[1]))
              continue;
            count--;
            uf.union(edge[0], edge[1]);
        }
      return count;
    }
}
class UnionFind {
    int[] root;
    int[] rank;
    
    UnionFind(int size) {
        root = new int[size];
        rank = new int[size];
        
        for(int i = 0; i < size; i++) {
            root[i] = i;
            rank[i] = 0;
        }
    }
    
    public int find(int x) {
        if(x == root[x])
            return x;
        return root[x] = find(root[x]);
    }
    
    public void union(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);
        
        if(rootX != rootY) {
            if(rank[rootX] > rank[rootY])
                root[rootY] = rootX;
            else if(rank[rootX] < rank[rootY])
                root[rootX] = rootY;
            else {
                root[rootY] = rootX;
                rank[rootX]++;
            }
        }
    }
    
    public boolean isConnected(int x, int y) {
        return find(x) == find(y);
    }
}
```
## Complexity Analysis
```
- Time Complexity: 
  - DFS: O(n)
  - Union Find: O(n)
- Space Complexity:
  - DFS: O(n+m)
  - Union Find: O(n)
```
