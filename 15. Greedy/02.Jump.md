# [55. Jump Game](https://leetcode.com/problems/jump-game/)
Medium

You are given an integer array nums. You are initially positioned at the array's first index, and each element in the array represents your maximum jump length at that position.

Return true if you can reach the last index, or false otherwise.

 

Example 1:
```
Input: nums = [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.
```
Example 2:
```
Input: nums = [3,2,1,0,4]
Output: false
Explanation: You will always arrive at index 3 no matter what. Its maximum jump length is 0, which makes it impossible to reach the last index.
 ```

Constraints:

- 1 <= nums.length <= 104
- 0 <= nums[i] <= 105

## Aprroach
```
- one variable(for eg. ans) is keeping upto which index can we move from the current index
- if ans value is less than the current index, which means we can't move to the current index
- at every index we check if you can better the ans, 
  which means if we can move to a higher index than the current index stored in ans
- if ans is sotring the value more than equal to the length of the given array
```
## Solution
```java
class Solution {
    public boolean canJump(int[] nums) {
        int ans = 0, n = nums.length;
        for(int i = 0; i < n-1; i++) {
            if(ans < i)
                return false;
            if(ans < i+nums[i])
                ans = i+nums[i];
            if(ans >= n-1)
                return true;
        }
        return ans >= n-1;
    }
}

```
## Complexity Analysis
```
- Time Complexity: O(N)
- Space Complexity: O(1)
```
