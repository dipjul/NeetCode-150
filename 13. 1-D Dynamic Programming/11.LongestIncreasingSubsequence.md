# [300. Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/)
Medium


Given an integer array nums, return the length of the longest strictly increasing subsequence.

A subsequence is a sequence that can be derived from an array by deleting some or no elements without changing the order of the remaining elements. For example, [3,6,2,7] is a subsequence of the array [0,3,1,6,2,2,7].

 

Example 1:
```
Input: nums = [10,9,2,5,3,7,101,18]
Output: 4
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4.
```
Example 2:
```
Input: nums = [0,1,0,3,2,3]
Output: 4
```
Example 3:
```
Input: nums = [7,7,7,7,7,7,7]
Output: 1
``` 

Constraints:

- 1 <= nums.length <= 2500
- -10<sup>4</sup> <= nums[i] <= 10<sup>4</sup>
 

> Follow up: Can you come up with an algorithm that runs in O(n log(n)) time complexity?

## Approach
```
- Starting from 2nd last element, lis[] will store 1 for all the elements
- compare it with the next element, if the next element is less than current element
  - add max of lis[curr], 1+lis[next]
```
## Solution
```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        int n = nums.length;
        int[] lis = new int[n];
        Arrays.fill(lis, 1);
        lis[n-1] = 1;
        int res = 1;
        for(int i = n-2; i >= 0; i--) {
            for(int j = i+1; j < n; j++) {
                if(nums[i] < nums[j])
                    lis[i] = Math.max(lis[i], 1+lis[j]);
            } 
            res = Math.max(res, lis[i]);
        }
        return res;
    }
}
```
## Complexity Analysis
```
- Time Complexity: O(n^2)
- Space Complexity: O(n)
```
