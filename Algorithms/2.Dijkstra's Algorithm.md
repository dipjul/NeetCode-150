# [2290. Minimum Obstacle Removal to Reach Corner](https://leetcode.com/problems/minimum-obstacle-removal-to-reach-corner/)
Hard


You are given a 0-indexed 2D integer array grid of size m x n. Each cell has one of two values:

- 0 represents an empty cell,
- 1 represents an obstacle that may be removed.
- You can move up, down, left, or right from and to an empty cell.

Return the minimum number of obstacles to remove so you can move from the upper left corner (0, 0) to the lower right corner (m - 1, n - 1).

 

Example 1:
```
Input: grid = [[0,1,1],[1,1,0],[1,1,0]]
Output: 2
Explanation: We can remove the obstacles at (0, 1) and (0, 2) to create a path from (0, 0) to (2, 2).
It can be shown that we need to remove at least 2 obstacles, so we return 2.
Note that there may be other ways to remove 2 obstacles to create a path.
```
Example 2:
```
Input: grid = [[0,1,0,0,0],[0,1,0,1,0],[0,0,0,1,0]]
Output: 0
Explanation: We can move from (0, 0) to (2, 4) without removing any obstacles, so we return 0.
``` 

Constraints:

- m == grid.length
- n == grid[i].length
- 1 <= m, n <= 105
- 2 <= m * n <= 105
- grid[i][j] is either 0 or 1.
- grid[0][0] == grid[m - 1][n - 1] == 0

## Approach
```
- Node class to store distance, row number, column number, done processing
- Map to store the key and the node for that key
- priority queue based on distance
- add the source to pq, with distance 0
- while pq not empty, poll a node
  - if node is not done
    - mark it done
    - check all it's neighbour's distance with the node.dsitance+grid[neighbour's row][neighbour's col]
    - update the distance of neighbour if it's greater than above calculated distance
    - and add the neighbour into the pq
```

## Solution
```java
class Solution {
    class Node {
        int dist;
        int i;
        int j;
        boolean done;
        Node(int d, int ii, int jj, boolean done) {
            dist = d;
            i = ii;
            j = jj;
            done = done;
        }
    }

    public int minimumObstacles(int[][] grid) {
        int[][] dirs = {{0,-1},{-1,0},{0,1},{1,0}};
        int n = grid.length, m = grid[0].length;
        PriorityQueue<Node> pq = new PriorityQueue<>((a, b)->a.dist-b.dist);
        Map<String, Node> mp = new HashMap<>();
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < m; j++) {
                String key = ""+i+","+j;
                Node node = null;
                if(i == 0 && j == 0)
                    node = new Node(0,i,j,false);
                else
                    node = new Node(100001,i,j,false);
                mp.put(key, node);
            }
        }

        pq.offer(mp.get("0,0"));
        while(!pq.isEmpty()) {
            Node node = pq.poll();
            if(node.done == false) {
                node.done = true;
                int i = node.i;
                int j = node.j;
                for(int[] dir:dirs) {
                    int new_i = i+dir[0];
                    int new_j = j+dir[1];
                    if(new_i >= 0 && new_i < n && new_j >= 0 && new_j < m) {
                        String neiK = ""+new_i+","+new_j;
                        Node nei = mp.get(neiK);
                        int cost = node.dist+grid[new_i][new_j];
                        if(cost < nei.dist) {
                            nei.dist = cost;
                            pq.offer(mp.get(neiK));
                        }
                    }
                }
            }

        }
        return mp.get(""+(n-1)+","+(m-1)).dist;
    }
}

```

## Complexity Analysis
```
- Time Complexity: O(n*m log (n*m))
- Space Complexity: O(n*m)
```
