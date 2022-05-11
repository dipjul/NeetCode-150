# [213. House Robber II](https://leetcode.com/problems/house-robber-ii/)
Medium


You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are arranged in a circle. That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have a security system connected, and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given an integer array nums representing the amount of money of each house, return the maximum amount of money you can rob tonight without alerting the police.

 

Example 1:
```
Input: nums = [2,3,2]
Output: 3
Explanation: You cannot rob house 1 (money = 2) and then rob house 3 (money = 2), because they are adjacent houses.
```
Example 2:
```
Input: nums = [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
Total amount you can rob = 1 + 3 = 4.
```
Example 3:
```
Input: nums = [1,2,3]
Output: 3
 ```

Constraints:

- 1 <= nums.length <= 100
- 0 <= nums[i] <= 1000

## Approach
Reference: [3. House Robber](https://github.com/dipjul/NeetCode-150/blob/d95d91ca2c7e0e25f421e3959ce0c0b62d9ba5a0/13.%201-D%20Dynamic%20Programming/3.HouseRobber.md)
```
- Reuse house robber, 1st time for [0, n-1] & 2nd time for [1, n]
- Return max out of them
```

## Solution
```java
class Solution {
    public int rob(int[] nums) {
        int n = nums.length;
        if(n == 1)
            return nums[0];
        if(n == 2)
            return Math.max(nums[0], nums[1]);
        int prev2 = nums[0];
        int prev1 = Math.max(nums[0], nums[1]);
        
        for(int i = 2; i < n-1; i++) {
            int temp = prev1;
            prev1 = Math.max(prev1, nums[i]+prev2);
            prev2 = temp;
        }
        int ans1 = prev1;
        prev2 = nums[1];
        prev1 = Math.max(nums[1], nums[2]);
        
        for(int i = 3; i < n; i++) {
            int temp = prev1;
            prev1 = Math.max(prev1, nums[i]+prev2);
            prev2 = temp;
        }
        int ans2 = prev1;
        return Math.max(ans1, ans2);
    }
}
```
## Complexity Analysis
```
- Time Complexity: O(2 * N) ~ O(N)
- Space Complexity: O(1)
```
