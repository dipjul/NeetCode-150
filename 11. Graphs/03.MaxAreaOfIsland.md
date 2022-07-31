# [695. Max Area of Island](https://leetcode.com/problems/max-area-of-island/)
Medium


You are given an m x n binary matrix grid. An island is a group of 1's (representing land) connected 4-directionally (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.

The area of an island is the number of cells with a value 1 in the island.

Return the maximum area of an island in grid. If there is no island, return 0.

 

Example 1:
```
Input: grid = [
[0,0,1,0,0,0,0,1,0,0,0,0,0],
[0,0,0,0,0,0,0,1,1,1,0,0,0],
[0,1,1,0,1,0,0,0,0,0,0,0,0],
[0,1,0,0,1,1,0,0,1,0,1,0,0],
[0,1,0,0,1,1,0,0,1,1,1,0,0],
[0,0,0,0,0,0,0,0,0,0,1,0,0],
[0,0,0,0,0,0,0,1,1,1,0,0,0],
[0,0,0,0,0,0,0,1,1,0,0,0,0]]
Output: 6
Explanation: The answer is not 11, because the island must be connected 4-directionally.
```
Example 2:
```
Input: grid = [[0,0,0,0,0,0,0,0]]
Output: 0
``` 

Constraints:

- m == grid.length
- n == grid[i].length
- 1 <= m, n <= 50
- grid[i][j] is either 0 or 1.

## Approach
```
- DFS
- count number of dfs call inside
```

## Solution
```java
class Solution {
    public int maxAreaOfIsland(int[][] grid) {
        boolean[][] mark = new boolean[grid.length][grid[0].length];
        int res = 0;

       for (int i = 0; i < grid.length; i++) {
           for (int j = 0; j < grid[0].length; j++) {
               if (!mark[i][j] && grid[i][j] == 1) {
                    res = Math.max(res, dfs(grid, i, j, mark));
               }
           }
       }
        return res;
    }

    private int dfs(int[][] grid, int i, int j, boolean[][] mark) {
        if (i < 0 || i >= grid.length || j < 0 || j >= grid[0].length || mark[i][j] || grid[i][j] == 0) {
            return 0;
        }
        mark[i][j] = true;
        return (1 + dfs(grid, i + 1, j, mark) +
        dfs(grid, i, j - 1, mark) +
        dfs(grid, i - 1, j, mark) +
        dfs(grid, i, j + 1, mark));
    }
}

```

## Complexity Analysis
```
- Time Complexity: O(n*m)
- Space Complexity: O(n*m)
```
