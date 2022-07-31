# [57. Insert Interval](https://leetcode.com/problems/insert-interval/)
Medium


You are given an array of non-overlapping intervals intervals where intervals[i] = [starti, endi] represent the start and the end of the ith interval and intervals is sorted in ascending order by starti. You are also given an interval newInterval = [start, end] that represents the start and end of another interval.

Insert newInterval into intervals such that intervals is still sorted in ascending order by starti and intervals still does not have any overlapping intervals (merge overlapping intervals if necessary).

Return intervals after the insertion.

 

Example 1:
```
Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
Output: [[1,5],[6,9]]
```
Example 2:
```
Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
Output: [[1,2],[3,10],[12,16]]
Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].
``` 

Constraints:

- 0 <= intervals.length <= 10<sup>4</sup>
- intervals[i].length == 2
- 0 <= starti <= endi <= 10<sup>5</sup>
- intervals is sorted by starti in ascending order.
- newInterval.length == 2
- 0 <= start <= end <= 10<sup>5</sup>

## Approach
```
- Step 1: while interval's end is lesser than new interval's start, keep adding it to result
- After step 1, we'll be at the position where new interval will start(either overlap or as the initial interval or as the last interval
- Step 2: while intervals's start is <= new interval's end
  - Keep taking the min start & max end and assign into the new interval(overlapping)
- After step 2, we'll have the merged new interval, add it to result
- Step 3: while intervals not finished processing
  - keep adding them to the result
```

## Solution
```java
class Solution {

    public int[][] insert(int[][] intervals, int[] newInterval) {
        if (intervals.length < 1) return new int[][] { newInterval };

        List<int[]> mergedList = new ArrayList<>();
        int index = 0;
        while (index < intervals.length && intervals[index][1] < newInterval[0]) mergedList.add(intervals[index++]);

        while (index < intervals.length && intervals[index][0] <= newInterval[1]) {
            newInterval[0] = Math.min(newInterval[0], intervals[index][0]);
            newInterval[1] = Math.max(newInterval[1], intervals[index][1]);
            index++;
        }
        mergedList.add(newInterval);

        while (index < intervals.length) mergedList.add(intervals[index++]);

        return mergedList.toArray(new int[mergedList.size()][]);
    }
}

```

## Complexity Analysis
```
- Time Complexity: O(n)
- Space Complexity: O(n)
```
