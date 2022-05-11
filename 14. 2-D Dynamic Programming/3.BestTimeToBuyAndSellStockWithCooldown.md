# [309. Best Time to Buy and Sell Stock with Cooldown](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)
Medium


You are given an array prices where prices[i] is the price of a given stock on the ith day.

Find the maximum profit you can achieve. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times) with the following restrictions:

After you sell your stock, you cannot buy stock on the next day (i.e., cooldown one day).
Note: You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

 

Example 1:
```
Input: prices = [1,2,3,0,2]
Output: 3
Explanation: transactions = [buy, sell, cooldown, buy, sell]
```
Example 2:
```
Input: prices = [1]
Output: 0
``` 

Constraints:

- 1 <= prices.length <= 5000
- 0 <= prices[i] <= 1000

## Approach
![image](https://user-images.githubusercontent.com/20329508/167283016-32563379-5dd2-4dd8-8734-2eef1b61807d.png)

```
- From the above options diagram
- we can have two states:
  - buying
  - selling
- for buying we can either sell or cooldown
- for selling state we must give cooldown before next buying
```

## Solution
```java
class Solution {
    public int maxProfit(int[] prices) {
        boolean buy = false;
        Map<String, Integer> mp = new HashMap<>();
        return helper(prices, 0, mp, true);
    }
    
    private int helper(int[] prices, int index, Map<String, Integer> mp, boolean buying) {
        if(index >= prices.length)
            return 0;
        if(mp.containsKey("("+index+","+buying+")"))
            return mp.get("("+index+","+buying +")");
        // in both the cases we have the cooldown
        int cooldown = helper(prices, index+1, mp, buying);
        if(buying) {
            int buy = helper(prices, index+1, mp, !buying) - prices[index];
            mp.put("("+index+","+buying +")", Math.max(cooldown, buy));
        } else {
            // we can't buy in next index so we pass the index+2
            int sell = helper(prices, index+2, mp, !buying) + prices[index];
            mp.put("("+index+","+buying +")", Math.max(cooldown, sell));
        }
        return mp.get("("+index+","+buying +")");
    }
}
```

## Complexity Analysis
```
- Time Complexity: O(N)
- Space Complexity: O(N)
```
