# 73. Set Matrix Zeroes
Medium

Given an m x n integer matrix matrix, if an element is 0, set its entire row and column to 0's.

You must do it in place.

 

Example 1:
```
Input: matrix = [[1,1,1],[1,0,1],[1,1,1]]
Output: [[1,0,1],[0,0,0],[1,0,1]]
```
Example 2:
```
Input: matrix = [[0,1,2,0],[3,4,5,2],[1,3,1,5]]
Output: [[0,0,0,0],[0,4,5,0],[0,3,1,0]]
 ```

Constraints:

- m == matrix.length
- n == matrix[0].length
- 1 <= m, n <= 200
- -2<sup>31</sup> <= matrix[i][j] <= 2<sup>31</sup> - 1
 

Follow up:

- A straightforward solution using O(mn) space is probably a bad idea.
- A simple improvement uses O(m + n) space, but still not the best solution.
- Could you devise a constant space solution?

## Approach
```
- Use the first row and column to keep track of zeroes
- Use one variable for the 0th row or 0 column depending upon our choice
```

## Solution
```java
class Solution {
    public void setZeroes(int[][] matrix) {
        int col0 = 1;
        int n = matrix.length, m = matrix[0].length;
        // first column
        for(int i = 0; i < n; i++) {
            if(matrix[i][0] == 0)
                col0 = 0;
        }
        // first row
        for(int i = 0; i < m; i++) {
            if(matrix[0][i] == 0)
                matrix[0][0] = 0;
        }
        // starting from (1,1)
        for(int i = 1; i < n; i++) {
            for(int j = 1; j < m; j++) {
                if(matrix[i][j] == 0) {
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                }
            }
        }
        
        for(int i = 1; i < n; i++) {
            for(int j = 1; j < m; j++) {
                if(matrix[i][0] == 0 || matrix[0][j] == 0)
                    matrix[i][j] = 0;
            }
        }
        
        if(matrix[0][0] == 0) {
            for(int i = 1; i < m; i++)
                matrix[0][i] = 0;
        }
        
        if(col0 == 0) {
            for(int i = 0; i < n; i++)
                matrix[i][0] = 0;
        }
    }
}

```

## Complexity Analysis
```
- Time Complexity: O(N), N : numbero of elements in the matrix
- Space Complexity: O(1)
```
