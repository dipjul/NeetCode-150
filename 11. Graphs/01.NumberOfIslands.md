# [200. Number of Islands](https://leetcode.com/problems/number-of-islands/)
Medium


Given an m x n 2D binary grid grid which represents a map of '1's (land) and '0's (water), return the number of islands.

An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

 

Example 1:
```
Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
Output: 1
```
Example 2:
```
Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
Output: 3
 ```

Constraints:

- m == grid.length
- n == grid[i].length
- 1 <= m, n <= 300
- grid[i][j] is '0' or '1'.

## Approach
```
- DFS
- number of time DFS called is the ans
```

## Soluiton
```java
class Solution {
    public int numIslands(char[][] grid) {
        boolean[][] mark = new boolean[grid.length][grid[0].length];
        int res = 0;
        for(int i = 0; i < grid.length; i++) {
            for(int j = 0; j < grid[0].length; j++) {
                if(!mark[i][j] && grid[i][j] == '1') {
                    res++;
                    dfs(grid, i, j, mark);
                }
            }
        }
        return res;
    }
    
    private void dfs(char[][] grid, int i, int j, boolean[][] mark) {
        if(i < 0 || i >= grid.length || j < 0 || j >= grid[0].length || mark[i][j] || grid[i][j] == '0')
            return;
        mark[i][j] = true;
        dfs(grid, i+1, j, mark);
        dfs(grid, i, j-1, mark);
        dfs(grid, i-1, j, mark);
        dfs(grid, i, j+1, mark);
    }
}
```

## Complexity Analysis
```
- Time Complexity: O(n*m)
- Space Complexity: O(n*m)
```
