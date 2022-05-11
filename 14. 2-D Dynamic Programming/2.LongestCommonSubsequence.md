# [1143. Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/)
Medium


Given two strings text1 and text2, return the length of their longest common subsequence. If there is no common subsequence, return 0.

A subsequence of a string is a new string generated from the original string with some characters (can be none) deleted without changing the relative order of the remaining characters.

For example, "ace" is a subsequence of "abcde".
A common subsequence of two strings is a subsequence that is common to both strings.

 

Example 1:
```
Input: text1 = "abcde", text2 = "ace" 
Output: 3  
Explanation: The longest common subsequence is "ace" and its length is 3.
```
Example 2:
```
Input: text1 = "abc", text2 = "abc"
Output: 3
Explanation: The longest common subsequence is "abc" and its length is 3.
```
Example 3:
```
Input: text1 = "abc", text2 = "def"
Output: 0
Explanation: There is no such common subsequence, so the result is 0.
 ```

Constraints:

- 1 <= text1.length, text2.length <= 1000
- text1 and text2 consist of only lowercase English characters.

## Approach
```
- Classic DP problem
- create a table, chars of one string as row and other as column
- fill out the value
- Formula that would appear
  - if chars are equal: dp[i][j] = 1 + dp[i-1][j-1], (diagonally prev element)
  - else: dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1]), max(top element, left element)

```

## Solution
```java
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        int n1 = text1.length(), n2 = text2.length();
        int[][] dp = new int[n1+1][n2+1];
        
        for(int i = 1; i <= n1; i++) {
            char c1 = text1.charAt(i-1);
            for(int j = 1; j <= n2; j++) {
                char c2 = text2.charAt(j-1);
                if(c1 == c2) {
                    dp[i][j] = 1 + dp[i-1][j-1];
                } else {
                    dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1]);
                }
            }
        }
        return dp[n1][n2];
    }
}
```

## Complexity Analysis
```
- Time Compolexity: O(N*M), N : length of string 1, M : length of string 2
- Space Complexity: O(N*M)
```
