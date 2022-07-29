# [178 · Graph Valid Tree](https://www.lintcode.com/problem/178/)
Medium

Given n nodes labeled from 0 to n - 1 and a list of undirected edges (each edge is a pair of nodes), write a function to check whether these edges make up a valid tree.

You can assume that no duplicate edges will appear in edges. Since all edges are undirected, [0, 1] is the same as [1, 0] and thus will not appear together in edges.


Example 1:
```
Input: n = 5 edges = [[0, 1], [0, 2], [0, 3], [1, 4]]
Output: true.
```
Example 2:
```
Input: n = 5 edges = [[0, 1], [1, 2], [2, 3], [1, 3], [1, 4]]
Output: false.
```

## Approach
```
- check if number of edges is equal to n-1 or not
  - if not equal return false;
- do dfs and put it in a set, size of set should be equal to number of nodes
```

## Solution
```java
public class Solution {
    /**
     * @param n: An integer
     * @param edges: a list of undirected edges
     * @return: true if it's a valid tree, or false
     */
    public boolean validTree(int n, int[][] edges) {
        // write your code here
        if(edges.length != n-1)
            return false;
        if(n == 0 || n == 1)
            return true;
        Set<Integer> mark = new HashSet<>();
        Map<Integer, List<Integer>> graph = new HashMap<>();
        
        for(int i = 0; i < edges.length; i++) {
            int n1 = edges[i][0];
            int n2 = edges[i][1];
            List<Integer> arr1 = graph.getOrDefault(n1, new ArrayList<>());
            arr1.add(n2);
            List<Integer> arr2 = graph.getOrDefault(n2, new ArrayList<>());
            arr2.add(n1);
            graph.put(n1, arr1);
            graph.put(n2, arr2);
        }
        dfs(graph, 0, mark);
        return mark.size() == n;
    }

    private void dfs(Map<Integer, List<Integer>> graph, int i, Set<Integer> mark) {
        mark.add(i);
        for(int node : graph.get(i)) {
            if(!mark.contains(node))
                dfs(graph, node, mark);
        }
    }
}
```

## Complexity Analysis
```
- Time Complexity: O(n*m)
- Space Complexity: O(n+m)
```
