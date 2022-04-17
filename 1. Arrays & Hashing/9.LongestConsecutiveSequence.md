# 128. Longest Consecutive Sequence
Medium

Given an unsorted array of integers nums, return the length of the longest consecutive elements sequence.

You must write an algorithm that runs in O(n) time.

 

Example 1:
```
Input: nums = [100,4,200,1,3,2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.
```
Example 2:
```
Input: nums = [0,3,7,2,5,8,4,6,0,1]
Output: 9
 ```

Constraints:

- 0 <= nums.length <= 10<sup>5</sup>
- -10<sup>9</sup> <= nums[i] <= 10<sup>9</sup>

```java
class Solution {
    public int longestConsecutive(int[] nums) {
        Set<Integer> set = new HashSet<>();
        int result = 0;
        for(int num : nums)
            set.add(num);
        int count = 0;
        for(int num : nums) {
            if(!set.contains(num-1)) {
                while(set.contains(num++))
                    count++;
                result = Math.max(result, count);
                count = 0;
            }
        }
        return result;
    }
}
```
