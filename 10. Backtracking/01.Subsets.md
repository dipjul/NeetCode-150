# [78. Subsets](https://leetcode.com/problems/subsets/)
Medium


Given an integer array nums of unique elements, return all possible subsets (the power set).

The solution set must not contain duplicate subsets. Return the solution in any order.

 
Example 1:
```
Input: nums = [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
```
Example 2:
```
Input: nums = [0]
Output: [[],[0]]
 ```

Constraints:

- 1 <= nums.length <= 10
- -10 <= nums[i] <= 10
- All the numbers of nums are unique.

## Approach
```
Backtracking:
- Either select the element or not
- recursive call
tmp.add(nums[index]);
backtrack(nums, index+1, tmp, ans);
tmp.remove(tmp.size()-1);
backtrack(nums, index+1, tmp, ans);
```

## Solution
```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<Integer> tmp = new ArrayList<>();
        List<List<Integer>> ans = new ArrayList<>();
        backtrack(nums, 0, tmp, ans);
        return ans;
    }
    
    private void backtrack(int[] nums, int index, List<Integer> tmp, List<List<Integer>> ans) {
        if(index > nums.length)
            return;
        if(index == nums.length) {
            ans.add(new ArrayList<>(tmp));
            return;
        }
        tmp.add(nums[index]);
        backtrack(nums, index+1, tmp, ans);
        tmp.remove(tmp.size()-1);
        backtrack(nums, index+1, tmp, ans);
    }
}
```

## Complexity Analysis
```
- Time Complexity: O(2^N)
- Space Complexity: O(N)
```
