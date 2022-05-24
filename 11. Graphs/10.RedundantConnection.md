# [684. Redundant Connection](https://leetcode.com/problems/redundant-connection/)
Medium


In this problem, a tree is an undirected graph that is connected and has no cycles.

You are given a graph that started as a tree with n nodes labeled from 1 to n, with one additional edge added. The added edge has two different vertices chosen from 1 to n, and was not an edge that already existed. The graph is represented as an array edges of length n where edges[i] = [ai, bi] indicates that there is an edge between nodes ai and bi in the graph.

Return an edge that can be removed so that the resulting graph is a tree of n nodes. If there are multiple answers, return the answer that occurs last in the input.

 

Example 1:
```
Input: edges = [[1,2],[1,3],[2,3]]
Output: [2,3]
```
Example 2:
```
Input: edges = [[1,2],[2,3],[3,4],[1,4],[1,5]]
Output: [1,4]
 ```

Constraints:

- n == edges.length
- 3 <= n <= 1000
- edges[i].length == 2
- 1 <= ai < bi <= edges.length
- ai != bi
- There are no repeated edges.
- The given graph is connected.

## Approach
Ref: [Union Find](https://github.com/dipjul/NeetCode-150/blob/e7002953ae531e571f4d148f591a265dda256d7d/Algorithms/1.UnionFind.md)
```
- Using UnionFind we'll check whether the nodes of the given edge are already connected without using the current edge
- if already connect which means this edge is reduntant
- else union the nodes of the current edge
```

## Solution
```java
class Solution {
    int[] parent;
    int[] rank;
    public int[] findRedundantConnection(int[][] edges) {
        int n = edges.length;
        init(n);
        int[] res = new int[2];
        for(int[] edge:edges) {
            if(!union(edge[0], edge[1]))
                res = new int[]{ edge[0], edge[1] };
        }
        return res;
    }
    
    private void init(int n) {
        parent = new int[n+1];
        rank = new int[n+1];
        for(int i = 1; i <= n; i++) {
            parent[i] = i;
            rank[i] = 1;
        }
    }
    
    private int find(int val) {
        while(val != parent[val]) {
            parent[val] = parent[parent[val]];
            val = parent[val];
        }
        return parent[val];
    }
    
    private boolean union(int x, int y) {
        int p1 = find(x);
        int p2 = find(y);
        if(p1 == p2)
            return false;
        if(rank[p1] > rank[p2]) {
            parent[p2] = p1;
            rank[p1] += rank[p2];
        } else {
            parent[p1] = p2;
            rank[p2] += rank[p1];
        }
        return true;
    }
}
```

## Complexity Analysis
```
- Time Complexity: O(n)
- Space Complexity: O(n)
```
