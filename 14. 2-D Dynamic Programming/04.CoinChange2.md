# [518. Coin Change 2](https://leetcode.com/problems/coin-change-2/)
Medium


You are given an integer array coins representing coins of different denominations and an integer amount representing a total amount of money.

Return the number of combinations that make up that amount. If that amount of money cannot be made up by any combination of the coins, return 0.

You may assume that you have an infinite number of each kind of coin.

The answer is guaranteed to fit into a signed 32-bit integer.

 

Example 1:
```
Input: amount = 5, coins = [1,2,5]
Output: 4
Explanation: there are four ways to make up the amount:
5=5
5=2+2+1
5=2+1+1+1
5=1+1+1+1+1
```
Example 2:
```
Input: amount = 3, coins = [2]
Output: 0
Explanation: the amount of 3 cannot be made up just with coins of 2.
```
Example 3:
```
Input: amount = 10, coins = [10]
Output: 1
``` 

Constraints:

- 1 <= coins.length <= 300
- 1 <= coins[i] <= 5000
- All the values of coins are unique.
- 0 <= amount <= 5000

## Approach
```
- Make a table and go through a example
- generic recursive formula:
  - dp[i][j] = dp[i-1][j] + dp[i][j-coin]
- take care of edge cases
```

## Solution
```java
class Solution {
    public int change(int amount, int[] coins) {
        int n = coins.length;
        int dp[][] = new int[n][amount+1];
        
        for(int i = 0; i < n; i++)
            dp[i][0] = 1;
        
        for(int i = 0; i < n; i++) {
            for(int j = 1; j <= amount; j++) {
                int val = j-coins[i];
                if(i > 0) {
                    if(val >= 0)  
                        dp[i][j] = dp[i-1][j] + dp[i][val];
                    else
                        dp[i][j] = dp[i-1][j];     
                }
                else {
                    if(val >= 0)
                        dp[i][j] = dp[i][val];
                    else
                        dp[i][j] = 0; 
                }
            }
        }
        
        return dp[n-1][amount];
    }
  
    // Consise
    public int change(int amount, int[] coins) {
        int[][] dp = new int[coins.length+1][amount+1];
        dp[0][0] = 1;
        
        for (int i = 1; i <= coins.length; i++) {
            dp[i][0] = 1;
            for (int j = 1; j <= amount; j++) {
                dp[i][j] = dp[i-1][j] + (j >= coins[i-1] ? dp[i][j-coins[i-1]] : 0);
            }
        }
        return dp[coins.length][amount];
    }
  
    // Optimal
    public int change(int amount, int[] coins) {
        int[] dp = new int[amount + 1];
        dp[0] = 1;
        for (int coin : coins) {
            for (int i = coin; i <= amount; i++) {
                dp[i] += dp[i-coin];
            }
        }
        return dp[amount];
    }
}

```

## Complexity Analysis
```
- Time Complexity: O(Amount*No. of coins)
- Space Complexity: 
  - 2D: O(Amount*No. of coins)
  - Optimal: O(Amount+1)
```
