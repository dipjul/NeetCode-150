# [51. N-Queens](https://leetcode.com/problems/n-queens/)
Hard

The n-queens puzzle is the problem of placing n queens on an n x n chessboard such that no two queens attack each other.

Given an integer n, return all distinct solutions to the n-queens puzzle. You may return the answer in any order.

Each solution contains a distinct board configuration of the n-queens' placement, where 'Q' and '.' both indicate a queen and an empty space, respectively.

 

Example 1:
```
Input: n = 4
Output: [[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]
Explanation: There exist two distinct solutions to the 4-queens puzzle as shown above
```
Example 2:
```
Input: n = 1
Output: [["Q"]]
``` 

Constraints:
- 1 <= n <= 9

## Approach
```
- Backtracking
- Used 3 boolean arrays to mark row, left diagonal and rightdiagonal
- r-c could be -ve so we add the n-1 to it
- for each column,
  -  we go through  each row and check whether we can place the queen or not
  - if possible then we place the column index at the row[]
  - recursive call to next column
```

## Solution
```java
// Do not try this at home
class Solution {
    int[] row;
    boolean[] rw, ld, rd;
    public List<List<String>> solveNQueens(int n) {
        row = new int[n];
        rw = new boolean[n];
        ld = new boolean[2*n-1];
        rd = new boolean[2*n-1];
        List<List<String>> ans = new ArrayList<>();
        backtrack(0, n, ans);
        return ans;
    }
    
    private void backtrack(int c, int n, List<List<String>> ans) {
        if(c == n) {
            ans.add(printer(row, n));
        }
        for(int r = 0; r < n; r++) {
            if(!rw[r] && !ld[r - c + n - 1] && !rd[r + c]) {
                rw[r] = ld[r - c + n - 1] = rd[r + c] = true;
                row[c] = r;
                backtrack(c+1,n,ans);
                rw[r] = ld[r - c + n - 1] = rd[r + c] = false;
            }
        }
    }
    
    private List<String> printer(int[] row, int n) {
        List<String> res = new ArrayList<>();
        for(int i = 0; i < n; i++) {
            StringBuilder sb = new StringBuilder(n);
            for(int j = 0; j < n; j++) {
                if(j == row[i])
                    sb.append('Q');
                else
                    sb.append('.');
            }
            res.add(sb.toString());
        }
        return res;
    }
}

```
## Complexity Analysis
```
- Time Complexity: O(n!)
- Space Complexity: O(n^2), building the result 
```
