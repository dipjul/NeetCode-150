# [130. Surrounded Regions](https://leetcode.com/problems/surrounded-regions/)
Medium


Given an m x n matrix board containing 'X' and 'O', capture all regions that are 4-directionally surrounded by 'X'.

A region is captured by flipping all 'O's into 'X's in that surrounded region.

 

Example 1:
```
Input: board = [
["X","X","X","X"],
["X","O","O","X"],
["X","X","O","X"],
["X","O","X","X"]]
Output: [
["X","X","X","X"],
["X","X","X","X"],
["X","X","X","X"],
["X","O","X","X"]]
Explanation: Surrounded regions should not be on the border, which means that any 'O' on the border of the board are not flipped to 'X'. Any 'O' that is not on the border and it is not connected to an 'O' on the border will be flipped to 'X'. Two cells are connected if they are adjacent cells connected horizontally or vertically.
```
Example 2:
```
Input: board = [["X"]]
Output: [["X"]]
 ```

Constraints:

- m == board.length
- n == board[i].length
- 1 <= m, n <= 200
- board[i][j] is 'X' or 'O'.

## Approach
```
- start dfs from all the boundaries
- mark all the cells that can be reach from the dfs as 1
- all those which were not marked 1 and in give board is "0", set them "X"
```

## Solution
```java
class Solution {
    public void solve(char[][] board) {
        int[][] mark = new int[board.length][board[0].length];
        for (int j = 0; j < board[0].length; j++) {
            if (board[0][j] == 'O')
                dfs(board, 0, j, mark);
        }
        for (int j = 0; j < board[0].length; j++) {
            if (board[board.length - 1][j] == 'O')
                dfs(board, board.length - 1, j, mark);
        }
        for (int j = 0; j < board.length; j++) {
            if (board[j][0] == 'O')
                dfs(board, j, 0, mark);
        }
        for (int j = 0; j < board.length; j++) {
            if (board[j][board[0].length - 1] == 'O')
                dfs(board, j, board[0].length - 1, mark);
        }
        for(int i = 0; i < board.length; i++) {
            for(int j = 0; j < board[0].length; j++) {
                if(mark[i][j] == 0 && board[i][j] == 'O')
                    board[i][j] = 'X';
            }
        }
    }

    private void dfs(char[][] grid, int i, int j, int[][] mark) {
        if (i < 0 || j < 0 || i >= grid.length || j >= grid[0].length || mark[i][j] == 1 || grid[i][j] == 'X')
            return;
        mark[i][j] = 1;
        dfs(grid, i, j - 1, mark);
        dfs(grid, i, j + 1, mark);
        dfs(grid, i - 1, j, mark);
        dfs(grid, i + 1, j, mark);
    }
}
```

## Complexity Analysis
```
- Time Complexity: O(m*n)
- Space Complexity: O(m*n)
```
