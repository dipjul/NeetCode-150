# [72. Edit Distance](https://leetcode.com/problems/edit-distance/)
Hard

Share
Given two strings word1 and word2, return the minimum number of operations required to convert word1 to word2.

You have the following three operations permitted on a word:

- Insert a character
- Delete a character
- Replace a character
 

Example 1:
```
Input: word1 = "horse", word2 = "ros"
Output: 3
Explanation: 
horse -> rorse (replace 'h' with 'r')
rorse -> rose (remove 'r')
rose -> ros (remove 'e')
```
Example 2:
```
Input: word1 = "intention", word2 = "execution"
Output: 5
Explanation: 
intention -> inention (remove 't')
inention -> enention (replace 'i' with 'e')
enention -> exention (replace 'n' with 'x')
exention -> exection (replace 'n' with 'c')
exection -> execution (insert 'u')
 ```

Constraints:

- 0 <= word1.length, word2.length <= 500
- word1 and word2 consist of lowercase English letters.

## Aproach
```
- make a table with one word as row and other as column,
  - append same char at the start of the both words to represent that both are empty string then 0 operation rqd to convert from word1 to word2
- generic recursive equation: 
  - dp[i][j] = dp[i-1][j-1], if char are same
  - dp[i][j] = 1 + min(dp[i-1][j], dp[i-1][j-1], dp[i][j-1]), i.e. 1 + min(left, top, diagonally prev)
- take care of base cases
```

## Solution
```java
class Solution {
    public int minDistance(String word1, String word2) {
        int m = word1.length(), n = word2.length();
        int dp[][] = new int[n+1][m+1];
        for(int i = 1; i <= n; i++) {
            dp[i][0] = i;
        }
        
        for(int i = 1; i <= m; i++) {
            dp[0][i] = i;
        }
        
        for(int i = 1; i <= n; i++) {
            char ch1 = word2.charAt(i-1);
            for(int j = 1; j <= m; j++) {
                char ch2 = word1.charAt(j-1);
                
                if(ch1 == ch2)
                    dp[i][j] = dp[i-1][j-1];
                else
                    dp[i][j] = 1 + Math.min(dp[i-1][j], Math.min(dp[i-1][j-1], dp[i][j-1]));
            }
        }
        
        return dp[n][m];
    }
}
```

## Complexity Analysis
```
- Time Complexity: O(len(word1)*len(word2))
- Space Complexity: O(len(word1)*len(word2))
```
