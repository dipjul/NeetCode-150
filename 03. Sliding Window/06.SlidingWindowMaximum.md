# [239. Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/)
Hard


You are given an array of integers nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position.

Return the max sliding window.

 

Example 1:
```
Input: nums = [1,3,-1,-3,5,3,6,7], k = 3
Output: [3,3,5,5,6,7]
Explanation: 
Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```
Example 2:
```
Input: nums = [1], k = 1
Output: [1]
``` 

Constraints:
- 1 <= nums.length <= 10<sup>5</sup>
- -10<sup>4</sup> <= nums[i] <= 10<sup>4</sup>
- 1 <= k <= nums.length

## Approach
```
- Use Deque, to keep the elements
- we'll keep the elemenet in decreasing order
- while the element at the first of the queue, i.e the index of the nums, 
    if it's out of the window, keep removing the element
- while the element at the last of the queue, i.e the index, 
    if it's less than equal to new element of the nums, keep removing the element
- insert the index of new element of nums
- if wE greater than k-1, then add the first element (index of the element in nums)
    of the queue to res
```

## Solution
```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        int[] res = new int[nums.length - k + 1];
        int wS = 0, s = 0;
        ArrayDeque<Integer> q = new ArrayDeque<>();
        
        for (int wE = 0; wE < nums.length; wE++) {
            // while the element at the first of the queue, i.e the index,
            // if it's out of the window, keep removing the element
            while(!q.isEmpty() && q.peekFirst() <= wE-k)
                q.pollFirst();
            
            // while the element at the last of the queue, i.e the index,
            // if it's less than equal to new element of the nums,
            // keep removing the element
            while(!q.isEmpty() && nums[q.peekLast()] <= nums[wE])
                q.pollLast();
          
            // insert the index of new element of nums
            q.offerLast(wE);
            
            // if wE greater than k-1, then add the first element
            // (index of the element in nums) of the queue to res
            if(wE >= k-1)
                res[s++] = nums[q.peekFirst()];
        }
        return res;
    }
}
```

## Complexity Analysis
```
- Time Complexity: O(n)
- Space Complexity: O(k), where k < n
```
