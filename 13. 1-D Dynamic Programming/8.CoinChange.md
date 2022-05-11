# [322. Coin Change](https://leetcode.com/problems/coin-change/)
Medium


You are given an integer array coins representing coins of different denominations and an integer amount representing a total amount of money.

Return the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

You may assume that you have an infinite number of each kind of coin.

 

Example 1:
```
Input: coins = [1,2,5], amount = 11
Output: 3
Explanation: 11 = 5 + 5 + 1
```
Example 2:
```
Input: coins = [2], amount = 3
Output: -1
```
Example 3:
```
Input: coins = [1], amount = 0
Output: 0
``` 

Constraints:

- 1 <= coins.length <= 12
- 1 <= coins[i] <= 2<sup>31</sup> - 1
- 0 <= amount <= 10<sup>4</sup>

## Approach
```
- we'll have dp array of size amount+1
- we'll initiaze the array with large value
- dp[0] would be 0
- for in range(1, amount)
  - for each coin
    - dp[i] = min(dp[i], 1 + dp[i-coin])
- dp[amount] will either have the ans or else it'll have the default value
```

## Solution
```java
class Solution {
   public int coinChange(int[] coins, int amount) {
        int[] dp = new int[amount + 1];
        Arrays.fill(dp, amount + 1);
        dp[0] = 0;
        for (int i = 1; i <= amount; i++) {
            for (int j = 0; j < coins.length; j++) {
                if (coins[j] <= i) {
                    dp[i] = Math.min(dp[i], dp[i - coins[j]] + 1);
                }
            }
        }
        return dp[amount] > amount ? -1 : dp[amount];
    }
}
```

## Complexity Analysis
```
- Time Complex: O(N*K), N: amount+1, K = coins.length
- Space complexity: O(N), N: amount+1
```
