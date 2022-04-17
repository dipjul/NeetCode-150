# 36. Valid Sudoku
Medium


Determine if a 9 x 9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

- Each row must contain the digits 1-9 without repetition.
- Each column must contain the digits 1-9 without repetition.
- Each of the nine 3 x 3 sub-boxes of the grid must contain the digits 1-9 without repetition.

Note:
- A Sudoku board (partially filled) could be valid but is not necessarily solvable.
- Only the filled cells need to be validated according to the mentioned rules.
 

Example 1:

```
Input: board = 
[["5","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: true
```
Example 2:
```
Input: board = 
[["8","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: false
```
Explanation: Same as Example 1, except with the 5 in the top left corner being modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.
 

Constraints:

- board.length == 9
- board[i].length == 9
- board[i][j] is a digit 1-9 or '.'.

```java
// My Solution
class Solution {
    public boolean isValidSudoku(char[][] board) {
        
        for(int i = 0; i < 9; i++) {
            for(int j = 0; j < 9; j++) {
                char c = board[i][j];
                if(isDigit(c) && !isValid(c, i, j, board)) {
                    return false;
                }
            }
        }
        
        return true;
    }
    
    private boolean isDigit(char c) {
        if(c-'0' > 9 || c-'0' < 0)
            return false;
        return true;
    }
    
    private boolean isValid(char c, int i, int j, char[][] board) {
        if(isValidRow(c, i, j, board) && isValidCol(c, i, j, board) && isValidGrid(c, i, j, board))
            return true;
        return false;
    }
    
    private boolean isValidRow(char c, int row, int col, char[][] board) {
        for(int i = 0; i < 9; i++) {
            if(board[row][i] == c && i != col)
                return false;
        }
        return true;
    }
    
    private boolean isValidCol(char c, int row, int col, char[][] board) {
        for(int i = 0; i < 9; i++) {
            if(board[i][col] == c && i != row)
                return false;
        }
        return true;
    }
    
    private boolean isValidGrid(char c, int row, int col, char[][] board) {
        int initialRow = 3*(row/3), initialCol = 3*(col/3);
        
        for(int i = initialRow; i < initialRow+3; i++) {
            for(int j = initialCol; j < initialCol+3; j++) {
                if(board[i][j] == c && i != row && j != col)
                    return false;
            }
        }
        return true;
    }
}
```
```java
// Using Set
public boolean isValidSudoku(char[][] board) {
    Set seen = new HashSet();
    for (int i=0; i<9; ++i) {
        for (int j=0; j<9; ++j) {
            char number = board[i][j];
            if (number != '.')
                if (!seen.add(number + " in row " + i) ||
                    !seen.add(number + " in column " + j) ||
                    !seen.add(number + " in block " + i/3 + "-" + j/3))
                    return false;
        }
    }
    return true;
}
```
