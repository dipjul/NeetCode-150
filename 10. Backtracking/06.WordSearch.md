# [79. Word Search](https://leetcode.com/problems/word-search/)
Medium


Given an m x n grid of characters board and a string word, return true if word exists in the grid.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

 

Example 1:
```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
Output: true
```
Example 2:
```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"
Output: true
```
Example 3:
```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"
Output: false
``` 

Constraints:

- m == board.length
- n = board[i].length
- 1 <= m, n <= 6
- 1 <= word.length <= 15
- board and word consists of only lowercase and uppercase English letters.
 
### Follow up: Could you use search pruning to make your solution faster with a larger board?

## Approach
```
Backtracking:
- 4 choices top, down, left & right moves
- mark the element we are accessing
- if we match the word, we get the ans
```

## Solution
```java
class Solution {
    public boolean exist(char[][] board, String word) {
        boolean[] res = new boolean[1];
        boolean[][] mark = new boolean[board.length][board[0].length];
        for(int i = 0; i < board.length; i++) {
            for(int j = 0; j < board[0].length; j++) {
                if(board[i][j] == word.charAt(0)) {
                    backtrack(board, word, mark, i, j, res);
                    if(res[0] == true)
                        return true;
                }
            }
        }
        return false;
    }
    
    private void backtrack(char[][] board, String word, boolean[][] mark, int i, int j, boolean[] res) {
        if (word.length() == 0) {
            res[0] = true;
            return;
        }
        if (i >= board.length || j >= board[0].length || i < 0 || j < 0 || mark[i][j])
            return;

        if (word.charAt(0) == board[i][j]) {
            mark[i][j] = true;
            if (i >= 0) {
                backtrack(board, word.substring(1), mark, i - 1, j, res);
            }
            if (j >= 0) {
                backtrack(board, word.substring(1), mark, i, j - 1, res);
            }
            if (i < board.length) {
                backtrack(board, word.substring(1), mark, i + 1, j, res);
            }
            if (j < board[0].length) {
                backtrack(board, word.substring(1), mark, i, j + 1, res);
            }
            mark[i][j] = false;
        }
    }
}
```
```java
// little optimized
class Solution {
    boolean[][] visited;
    public boolean exist(char[][] board, String word) {
        int rows = board.length;
        int cols = board[0].length;
        visited = new boolean[rows][cols];
        
        for(int i = 0; i < rows; i++) {
            for(int j = 0; j < cols; j++) {
                if(word.charAt(0) == board[i][j] && search(i, j, 0, word, board))
                    return true;
            }
        }
        return false;
    }
    
    public boolean search(int i, int j, int index, String word, char[][] board) {
        if(index == word.length())
            return true;
        
        if(i < 0 || i >= board.length || j < 0 || j >= board[0].length || word.charAt(index) != board[i][j] || visited[i][j]) {
            return false;
        }
        
        visited[i][j] = true;
        
        if(
            search(i+1, j, index+1, word, board) ||
            search(i-1, j, index+1, word, board) ||
            search(i, j+1, index+1, word, board) ||
            search(i, j-1, index+1, word, board)
        ) {
            return true;
        }
        
        visited[i][j] = false;
        return false;
    }
}
```
## Complexity Analysis
```
- Time Complexity: O(4^N)
- Space Complexity: O(N)
```
