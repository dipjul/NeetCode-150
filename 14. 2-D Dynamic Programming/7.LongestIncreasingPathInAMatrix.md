# [329. Longest Increasing Path in a Matrix](https://leetcode.com/problems/longest-increasing-path-in-a-matrix/)
Hard


Given an m x n integers matrix, return the length of the longest increasing path in matrix.

From each cell, you can either move in four directions: left, right, up, or down. You may not move diagonally or move outside the boundary (i.e., wrap-around is not allowed).

 

Example 1:
```
Input: matrix = [[9,9,4],[6,6,8],[2,1,1]]
Output: 4
Explanation: The longest increasing path is [1, 2, 6, 9].
```
Example 2:
```
Input: matrix = [[3,4,5],[3,2,6],[2,2,1]]
Output: 4
Explanation: The longest increasing path is [3, 4, 5, 6]. Moving diagonally is not allowed.
```
Example 3:
```
Input: matrix = [[1]]
Output: 1
 ```

Constraints:

- m == matrix.length
- n == matrix[i].length
- 1 <= m, n <= 200
- 0 <= matrix[i][j] <= 2<sup>31</sup> - 1

## Approach
```
- DFS/backtracking with DP
- Start from each element in the matrix
- Find the longest increasing path we can make from that position
  - by moving towards the 4 directions 
- Store the result in a table
- Reuse the value
```

## Solution
```java
class Solution {
    
    public int longestIncreasingPath(int[][] matrix) {
        int[][] cache = new int[matrix.length][matrix[0].length];
        int res = 1;
        for(int i = 0; i < matrix.length; i++) {
            for(int j = 0; j < matrix[0].length; j++)
                res = Math.max(res, backtrack(matrix, i, j, -1, cache));
        }
        return res;
    }
    
    private int backtrack(int[][] matrix, int i, int j, int prev, int[][] cache) {
        if(i < 0 || j < 0 || i >= matrix.length || j >= matrix[0].length || prev >= matrix[i][j])
            return 0;
        
        if(cache[i][j] != 0)
            return cache[i][j];
        
        int max = 1;
        
        max = Math.max(max, 1 + backtrack(matrix, i-1, j, matrix[i][j], cache));
        max = Math.max(max, 1 + backtrack(matrix, i, j-1, matrix[i][j], cache));
        max = Math.max(max, 1 + backtrack(matrix, i+1, j, matrix[i][j], cache));
        max = Math.max(max, 1 + backtrack(matrix, i, j+1, matrix[i][j], cache));

        cache[i][j] = max;
        return max;
    }
}
```

## Complexity Analysis
```
- Time Complexity: dfs: O(n*m), we'll go through each position, after that it'll return from any position in O(1)
- Space Complexity: O(n*m) 
```
