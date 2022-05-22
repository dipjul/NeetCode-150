# [417. Pacific Atlantic Water Flow]()
Medium


There is an m x n rectangular island that borders both the Pacific Ocean and Atlantic Ocean. The Pacific Ocean touches the island's left and top edges, and the Atlantic Ocean touches the island's right and bottom edges.

The island is partitioned into a grid of square cells. You are given an m x n integer matrix heights where heights[r][c] represents the height above sea level of the cell at coordinate (r, c).

The island receives a lot of rain, and the rain water can flow to neighboring cells directly north, south, east, and west if the neighboring cell's height is less than or equal to the current cell's height. Water can flow from any cell adjacent to an ocean into the ocean.

Return a 2D list of grid coordinates result where result[i] = [ri, ci] denotes that rain water can flow from cell (ri, ci) to both the Pacific and Atlantic oceans.

 

Example 1:
```
Input: heights = [[1,2,2,3,5],[3,2,3,4,4],[2,4,5,3,1],[6,7,1,4,5],[5,1,1,2,4]]
Output: [[0,4],[1,3],[1,4],[2,2],[3,0],[3,1],[4,0]]
```
Example 2:
```
Input: heights = [[2,1],[1,2]]
Output: [[0,0],[0,1],[1,0],[1,1]]
``` 

Constraints:

- m == heights.length
- n == heights[r].length
- 1 <= m, n <= 200
- 0 <= heights[r][c] <= 10<sup>5</sup>

## Approach
```
- dfs: start from all the boundary along with respective set for pacific and atlantic
- intersection of both set
```

## Solution
```java
class Solution {

    public List<List<Integer>> pacificAtlantic(int[][] heights) {
        List<List<Integer>> res = new ArrayList<>();
        Set<String> pacific = new HashSet<>();
        Set<String> atlantic = new HashSet<>();
        int rows = heights.length, cols = heights[0].length;
        for (int i = 0; i < cols; i++) {
            dfs(heights, 0, i, pacific, heights[0][i]);
            dfs(heights, rows-1, i, atlantic, heights[rows-1][i]);
        }
        for (int i = 0; i < rows; i++) {
            dfs(heights, i, 0, pacific, heights[i][0]);
            dfs(heights, i, cols-1, atlantic, heights[i][cols-1]);
        }
        pacific.retainAll(atlantic);
        for (String s : pacific) {
            String[] arr = s.split(",");
            List<Integer> a = new ArrayList<>();
            a.add(Integer.parseInt(arr[0]));
            a.add(Integer.parseInt(arr[1]));
            res.add(a);
        }
        return res;
    }

    private void dfs(int[][] grid, int i, int j, Set<String> visited, int prev) {
        if (i < 0 || j < 0 || i >= grid.length || j >= grid[0].length || grid[i][j] < prev || visited.contains(i + "," + j)) return;

        visited.add(i + "," + j);
        dfs(grid, i, j - 1, visited, grid[i][j]);
        dfs(grid, i, j + 1, visited, grid[i][j]);
        dfs(grid, i - 1, j, visited, grid[i][j]);
        dfs(grid, i + 1, j, visited, grid[i][j]);
    }
}

```

## Complexity Analysis
```
- Time Complexity: O(m*n)
- Space Complexity: O(m*n)
```
