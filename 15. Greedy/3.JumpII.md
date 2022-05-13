# [45. Jump Game II](https://leetcode.com/problems/jump-game-ii/)
Medium


Given an array of non-negative integers nums, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

You can assume that you can always reach the last index.

 

Example 1:
```
Input: nums = [2,3,1,1,4]
Output: 2
Explanation: The minimum number of jumps to reach the last index is 2. Jump 1 step from index 0 to 1, then 3 steps to the last index.
```
Example 2:
```
Input: nums = [2,3,0,1,4]
Output: 2
 ```

Constraints:

- 1 <= nums.length <= 104
- 0 <= nums[i] <= 1000

## Approach
```
- dp array initialized to large value, later on it will store the min jumps required to reach last index from each index
- we start from end, second last index, try to see if we can move to the last index
- for each index you look for the min step we need to reach last index
- Pattern:
  - for each nums's index(i):
    - for range(0,num) (j):
      - dp[i] = min(dp[i], 1 + dp[i+j]   
```
### TODO : Optimization

## Solution
```java
class Solution {
    public int jump(int[] nums) {
        int n = nums.length;
        int dp[] = new int[n];
        Arrays.fill(dp, 10000);
        dp[n - 1] = 0;

        for (int i = n - 2; i >= 0; i--) {
            for (int j = nums[i]; j >= 0; j--) {
                if (i + j < n)
                    dp[i] = Math.min(dp[i], 1 + dp[i + j]);
            }
        }
        return dp[0];
    }
}

```

## Complexity Analysis
```
- Time Complexity: O(k*N)
- Space Complexity: O(N)
```
