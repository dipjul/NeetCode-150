# [435. Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/)
Medium


Given an array of intervals intervals where intervals[i] = [starti, endi], return the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping.

 

Example 1:
```
Input: intervals = [[1,2],[2,3],[3,4],[1,3]]
Output: 1
Explanation: [1,3] can be removed and the rest of the intervals are non-overlapping.
```
Example 2:
```
Input: intervals = [[1,2],[1,2],[1,2]]
Output: 2
Explanation: You need to remove two [1,2] to make the rest of the intervals non-overlapping.
```
Example 3:
```
Input: intervals = [[1,2],[2,3]]
Output: 0
Explanation: You don't need to remove any of the intervals since they're already non-overlapping.
 ```

Constraints:

- 1 <= intervals.length <= 10<sup>5</sup>
- intervals[i].length == 2
- -5 * 10<sup>4</sup> <= starti < endi <= 5 * 10<sup>4</sup>

## Approach
```
- Sort the intervals by end time
- store the first interval (we're storing it as prev)
- loop through the intervals starting the 2nd interval
  - if current interval overlap with prev the increment the count
  - else assign the current interval to the prev
```

## Solution
```java
class Solution {
    public int eraseOverlapIntervals(int[][] intervals) {
        if(intervals.length <= 1)
            return 0;
        Arrays.sort(intervals, (a,b)->a[1]-b[1]);
        
        int count = 0;
        int[] prev = intervals[0];
        for(int i = 1; i < intervals.length; i++) {
            int[] curr = intervals[i];
            if(prev[1] > curr[0])
                count++;
            else
                prev = intervals[i];
        }
        
        return count;
    }
}

```

## Complexity Analysis
```
- Time Complexity: O(nlogn)
- Space Complexity: O(1)
```
