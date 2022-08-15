# [4. Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/)
Hard


Given two sorted arrays nums1 and nums2 of size m and n respectively, return the median of the two sorted arrays.

The overall run time complexity should be O(log (m+n)).

 

Example 1:
```
Input: nums1 = [1,3], nums2 = [2]
Output: 2.00000
Explanation: merged array = [1,2,3] and median is 2.
```
Example 2:
```
Input: nums1 = [1,2], nums2 = [3,4]
Output: 2.50000
Explanation: merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.
 ```

Constraints:
- nums1.length == m
- nums2.length == n
- 0 <= m <= 1000
- 0 <= n <= 1000
- 1 <= m + n <= 2000
- -10<sup>6</sup> <= nums1[i], nums2[i] <= 10<sup>6</sup>

## Approach

## Solution
```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        if(nums1.length > nums2.length)
            return findMedianSortedArrays(nums2, nums1);
        int total = nums1.length + nums2.length;
        int half = (total + 1) / 2;
        int l = 0, r = nums1.length;
        double result = 0d;
        while(l <= r) {
            int i = l + (r - l) / 2;
            int j = half - i;
            int nums1L = i > 0 ? nums1[i-1]:Integer.MIN_VALUE;
            int nums1R = i < nums1.length ? nums1[i]:Integer.MAX_VALUE;
            int nums2L = j > 0 ? nums2[j-1]:Integer.MIN_VALUE;
            int nums2R = j < nums2.length ? nums2[j]:Integer.MAX_VALUE;
            
            if(nums1L <= nums2R && nums2L <= nums1R) {
                if(total % 2 == 0) {
                    return (Math.max(nums1L, nums2L) + Math.min(nums1R, nums2R)) / 2.0;
                } else {
                    return Math.max(nums1L, nums2L);
                }
            } else if(nums1L > nums2R) {
                r = i - 1;
            } else {
                l = i + 1;
            }
        }
        return result;
    }
}
```

## Complexity Analysis
```
- Time Complexity: O(log(m+n))
- Space Complexity: O(1)
```
