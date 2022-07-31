# [39. Combination Sum](https://leetcode.com/problems/combination-sum/)
Medium


Given an array of distinct integers candidates and a target integer target, return a list of all unique combinations of candidates where the chosen numbers sum to target. You may return the combinations in any order.

The same number may be chosen from candidates an unlimited number of times. Two combinations are unique if the frequency of at least one of the chosen numbers is different.

It is guaranteed that the number of unique combinations that sum up to target is less than 150 combinations for the given input.

 

Example 1:
```
Input: candidates = [2,3,6,7], target = 7
Output: [[2,2,3],[7]]
Explanation:
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.
7 is a candidate, and 7 = 7.
These are the only two combinations.
```
Example 2:
```
Input: candidates = [2,3,5], target = 8
Output: [[2,2,2,2],[2,3,3],[3,5]]
```
Example 3:
```
Input: candidates = [2], target = 1
Output: []
 ```

Constraints:

- 1 <= candidates.length <= 30
- 1 <= candidates[i] <= 200
- All elements of candidates are distinct.
- 1 <= target <= 500

## Approach
```
Backtrack:
 - We can choose any of the element present in the array(n choices)
 - In subsets, we have only 2 choices
- Looping through elements to create a n way recursive call
for(int i = index; i < nums.length; i++) {
    tmp.add(nums[i]);
    backtrack(nums, i, tmp, ans, target - nums[i]);
    tmp.remove(tmp.size()-1);
}
```

## Solution
```java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> res = new ArrayList<>();
        backtrack(candidates, 0, new ArrayList<>(), res, target);

        return res;
    }
    
    private void backtrack(int[] nums, int index, List<Integer> tmp, List<List<Integer>> ans, int target) {
        if(index >= nums.length || target < 0)
            return;
        if(target == 0) {
            ans.add(new ArrayList<>(tmp));
            return;
        }
        
        for(int i = index; i < nums.length; i++) {
            tmp.add(nums[i]);
            backtrack(nums, i, tmp, ans, target - nums[i]);
            tmp.remove(tmp.size()-1);
        }
    }
}
```

## Complexity Analysis
```
- Time Complexity: O(N^N)
- Space Complexity: O(N)
```
