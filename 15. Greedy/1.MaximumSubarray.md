# 53. Maximum Subarray
Easy


Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

A subarray is a contiguous part of an array.

 

Example 1:
```
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```
Example 2:
```
Input: nums = [1]
Output: 1
```
Example 3:
```
Input: nums = [5,4,-1,7,8]
Output: 23
 ```

Constraints:

- 1 <= nums.length <= 105
- -104 <= nums[i] <= 104
 

### Follow up: If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int n = nums.length;
        
        int total = 0;
        int result = nums[0];
        
        for(int num : nums) {
            if(total < 0)
                total = 0;
            total = total+num;
            result = Math.max(result, total);
            
        }
        
        return result;
    }
}
```
