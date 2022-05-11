# [62. Unique Paths](https://leetcode.com/problems/unique-paths/)
Medium


There is a robot on an m x n grid. The robot is initially located at the top-left corner (i.e., grid[0][0]). The robot tries to move to the bottom-right corner (i.e., grid[m - 1][n - 1]). The robot can only move either down or right at any point in time.

Given the two integers m and n, return the number of possible unique paths that the robot can take to reach the bottom-right corner.

The test cases are generated so that the answer will be less than or equal to 2 * 109.

 

Example 1:
```
Input: m = 3, n = 7
Output: 28
```
Example 2:
```
Input: m = 3, n = 2
Output: 3
Explanation: From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Down -> Down
2. Down -> Down -> Right
3. Down -> Right -> Down
 ```

Constraints:

- 1 <= m, n <= 100

## Approach
```
- Last row and last column would have only one way
- others:
  - dp[i][j] = dp[i+1][j]+dp[i][j+1];
- dp[0][0] would have the result
```

## Solution
```java
class Solution {
    public int uniquePaths(int m, int n) {
        int[][] dp = new int[m][n];
        // last column
        for(int i = 0; i < m; i++) {
            dp[i][n-1] = 1;
        }
        // last row
        for(int i = 0; i < n; i++) {
            dp[m-1][i] = 1;
        }
        
        for(int i = m-2; i >= 0; i--) {
            for(int j = n-2; j >= 0; j--) {
                dp[i][j] = dp[i+1][j]+dp[i][j+1];
            }
        }
        return dp[0][0];
    }
}
```

## Complexity Analysis
```
- Time Complexity: O(m*n)
- Space Complexity: O(m*n)
```
