# [152. Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/)
Medium


Given an integer array nums, find a contiguous non-empty subarray within the array that has the largest product, and return the product.

The test cases are generated so that the answer will fit in a 32-bit integer.

A subarray is a contiguous subsequence of the array.

 

Example 1:
```
Input: nums = [2,3,-2,4]
Output: 6
Explanation: [2,3] has the largest product 6.
```
Example 2:
```
Input: nums = [-2,0,-1]
Output: 0
Explanation: The result cannot be 2, because [-2,-1] is not a subarray.
 ```

Constraints:

- 1 <= nums.length <= 2 * 10<sup>4</sup>
- -10 <= nums[i] <= 10
- The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.

## Approach
```
- two variable to keep max & min at that index
- result, initially stores the max element present in the array
- if we encounter 0, min and max set to 1
- else 
  - min = min(min*arr[i],max*arr[i],arr[i])
  - max = max(prevMin*arr[i], max*arr[i], arr[i])
  - result = max(max, result)
```

## Solution
```java
class Solution {
    public int maxProduct(int[] nums) {
        int n = nums.length;
        int min = nums[0], max = nums[0];
        int result = nums[0];

        for(int i = 1; i < n; i++)
            result = Math.max(result, nums[i]);
        
        for(int i = 1; i < n; i++) {
            if(nums[i] == 0) {
                min = 1;
                max = 1;
            } else {
                int tmp1 = min;
                min = Math.min(min*nums[i], Math.min(max*nums[i], nums[i]));
                max = Math.max(tmp1*nums[i], Math.max(max*nums[i], nums[i]));
                result = Math.max(result, max);
            }
        }
        
        return result;
    }
}
```

## Complexity Analysis
```
- Time Complexity: O(N)
- Space Complexity: O(1)
```
