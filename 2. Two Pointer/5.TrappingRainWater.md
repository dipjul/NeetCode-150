# [42. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/)
Hard


Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.

 

Example 1:
```
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. 
In this case, 6 units of rain water (blue section) are being trapped.
```
Example 2:
```
Input: height = [4,2,0,3,2,5]
Output: 9
 ```

Constraints:

- n == height.length
- 1 <= n <= 2 * 10<sup>4</sup>
- 0 <= height[i] <= 10<sup>5</sup>

## Approach
### First Approach:
```
- leftMax array to keep the max element on the left of the index
- rightMax array to keep the max element on the right of the index
- at each index take the min(leftMax, rightMax) - heigh[index], if it's greater than 0 add it to ans
- Time : O(N)
- Space: O(N)
```
### Second Approach:
```
- instead of keep arrays to store the leftmax & rightMax, we can use two variables
- if leftMax <= rightMax
  - try to update leftMax
  - if min(leftMax, rightMax) - heigh[index] > 0, add it to ans
  - move the left pointer ahead
- else
  - same as above just replacing the left's by right
  - decrement the right pointer
```
## Solution
```java
class Solution {
    public int trap(int[] height) {
        int left = 0, right = height.length-1;
        int lMax = height[0], rMax = height[right];
        int ans = 0;
        while(left <= right) {
            if(lMax <= rMax) {
                lMax = Math.max(lMax, height[left]);
                int val = Math.min(lMax, rMax)-height[left];
                ans += val < 0 ? 0 : val;
                left++;
            } else {
                rMax = Math.max(rMax, height[right]);
                int val = Math.min(lMax, rMax)-height[right];
                ans += val < 0 ? 0 : val;
                right--;
            }
        }       
        return ans;
    }
}

```
## Complexity Analysis
```
- Time Complexity: O(N) -> go through each elements of the height array
- Space Complexity: O(1)
```
