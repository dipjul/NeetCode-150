# [56. Merge Intervals](https://leetcode.com/problems/merge-intervals/)
Medium


Given an array of intervals where intervals[i] = [starti, endi], merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

 

Example 1:
```
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].
```
Example 2:
```
Input: intervals = [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.
 ```

Constraints:

- 1 <= intervals.length <= 10<sup>4</sup>
- intervals[i].length == 2
- 0 <= starti <= endi <= 10<sup>4</sup>

## Approach
```
- Sort the intervals by start time
- Use arr to store the merged list
- Start by inserting the first element
- looping through all the other intervals
  - check if last interval inserted into arr overlapped with current interval
  - if yes then create a new interval and push to arr
  - else insert the current interval to arr
```
## Solution
```java
class Solution {
    public int[][] merge(int[][] intervals) {
        Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
        List<int[]> arr = new ArrayList<>();
        arr.add(intervals[0]);
        int start = intervals[0][0];
        int end = intervals[0][1];
        for (int i = 1; i < intervals.length; i++) {
            int[] curr = intervals[i];
            int[] prev = arr.get(arr.size() - 1);
            if (curr[0] <= prev[1]) {
                arr.remove(arr.size() - 1);
                start = Math.min(curr[0], prev[0]);
                end = Math.max(curr[1], prev[1]);
                arr.add(new int[]{start, end});
            } else {
                arr.add(curr);
            }
        }
        return arr.toArray(new int[arr.size()][]);
    }
}
```
## Complexity Analysis
```
- Time Complexity: O(nlogn)
- Space Complexity: O(n), for arr
```
