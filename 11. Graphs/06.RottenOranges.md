# [994. Rotting Oranges](https://leetcode.com/problems/rotting-oranges/)
Medium


You are given an m x n grid where each cell can have one of three values:

- 0 representing an empty cell,
- 1 representing a fresh orange, or
- 2 representing a rotten orange.
- 
Every minute, any fresh orange that is 4-directionally adjacent to a rotten orange becomes rotten.

Return the minimum number of minutes that must elapse until no cell has a fresh orange. If this is impossible, return -1.

 

Example 1:
```
Input: grid = [[2,1,1],[1,1,0],[0,1,1]]
Output: 4
```
Example 2:
```
Input: grid = [[2,1,1],[0,1,1],[1,0,1]]
Output: -1
Explanation: The orange in the bottom left corner (row 2, column 0) is never rotten, because rotting only happens 4-directionally.
```
Example 3:
```
Input: grid = [[0,2]]
Output: 0
Explanation: Since there are already no fresh oranges at minute 0, the answer is just 0.
 ```

Constraints:

- m == grid.length
- n == grid[i].length
- 1 <= m, n <= 10
- grid[i][j] is 0, 1, or 2.

## Approaches
```
- Implementation of Topological Sort
- Insert all the rotten tomatoes inside the queue as sources
- have an fresh tomato count
- while sources queue not empty,
  - we pull one pos at a time and check it's neighbour if there is any fresh tomato
  - if we found fresh tomato, we make it rotten and add to our sources queue, decrement the fresh count
  - for each run of while loop,
    - we check if the sources is not empty, increment the time
```

## Solution
```java
class Solution {
    public int orangesRotting(int[][] grid) {
        int[][] dirs = {{-1, 0}, {1, 0}, {0, -1}, {0, 1} };
        Queue<int[]> q = new LinkedList<>();
        int n = grid.length, m = grid[0].length;
        int countFresh = 0;
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < m; j++) {
                if(grid[i][j] == 1)
                    countFresh++;
                if(grid[i][j] == 2)
                    q.offer(new int[]{i, j});
            }
        }
        
        if(countFresh == 0) return 0;
        int time = 0;
        while(!q.isEmpty()) {
            int size = q.size();
            for(int i = 0; i < size; i++) {
                int[] currPos = q.poll();
                int currI = currPos[0], currJ = currPos[1];
                for(int[] dir : dirs) {
                    if(currI+dir[0] < 0 || currJ+dir[1] < 0 || currI+dir[0] >= n || currJ+dir[1] >= m || grid[currI+dir[0]][currJ+dir[1]] != 1)
                        continue;
                    if(grid[currI+dir[0]][currJ+dir[1]] == 1) {
                        grid[currI+dir[0]][currJ+dir[1]] = 2;
                        q.offer(new int[]{currI+dir[0], currJ+dir[1]});
                        countFresh--;                        
                    }
                }

            }
            if(!q.isEmpty())
                time++;
            
        }
        return countFresh!=0?-1:time;
    }
}
```

## Complexity Analysis
```
- Time Complexity: O(n*m)
- Space Complexity: O(n*m)
```
