# [919 · Meeting Rooms II]()
Medium

Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...] (si < ei), find the minimum number of conference rooms required.)

> (0,8),(8,10) is not conflict at 8


Example 1
```
Input: intervals = [(0,30),(5,10),(15,20)]
Output: 2
Explanation:
We need two meeting rooms
room1: (0,30)
room2: (5,10),(15,20)
```
Example2 
```
Input: intervals = [(2,7)]
Output: 1
Explanation: 
Only need one meeting room
```

## Approach
```
Approach 1:
  - Create a array of size, largest element - smallest element + 1
  - for each interval:
    - increment all the index between [start, end)
    - keep tracking the max element in that array, that's the answer

Approach 2(Better):
  - Sort starting time and ending seperatedly
  - Two pointers one from traversing through the start[] and the other through the end[]
  - keep track of max count(it would have the answer)
  - if pointer pointing at start < pointer pointing at end
    - increment the count & move the start pointer forward
  - else
    - decrement the count & move the end pointer forward
```

## Solution
```java
/**
 * Definition of Interval:
 * public class Interval {
 *     int start, end;
 *     Interval(int start, int end) {
 *         this.start = start;
 *         this.end = end;
 *     }
 * }
 */

public class Solution {
    /**
     * @param intervals: an array of meeting time intervals
     * @return: the minimum number of conference rooms required
     */
    public int minMeetingRooms(List<Interval> intervals) {
        // Write your code here
        if(intervals == null || intervals.size() == 0)
            return 0;
        int rooms = 0;
        int max = intervals.get(0).end;
        int min = intervals.get(0).start;

        for(int i = 1; i < intervals.size(); i++) {
            max = Math.max(max, intervals.get(i).end);
            min = Math.min(min, intervals.get(i).start);
        }
        int[] arr = new int[max-min+1];
        for(Interval interval: intervals) {
            int s = interval.start-min;
            int e = interval.end-min;
            for(int i = s; i < e; i++) {
                arr[i]++;
                rooms = Math.max(rooms, arr[i]);
            }
        }
        return rooms;
    }
}

```
```java
// Better Solution
public class Solution {
    public int minMeetingRooms(List<Interval> intervals) {
    // Check for the base case. If there are no intervals, return 0
    if (intervals.size() == 0) {
      return 0;
    }

    Integer[] start = new Integer[intervals.size()];
    Integer[] end = new Integer[intervals.size()];

    for (int i = 0; i < intervals.size(); i++) {
      start[i] = intervals.get(i).start;
      end[i] = intervals.get(i).end;
    }

    // Sort the intervals by end time
    Arrays.sort(end);

    // Sort the intervals by start time
    Arrays.sort(start);

    // The two pointers in the algorithm: e_ptr and s_ptr.
    int startPointer = 0, endPointer = 0;

    // Variables to keep track of maximum number of rooms used.
    int usedRooms = 0, count = 0;

    // Iterate over intervals.
    while (startPointer < intervals.size()) {

      // If there is a meeting that has started before the time 
      // the meeting at `end_pointer` starts means overlapping
      if (start[startPointer] < end[endPointer]) {
        count += 1;
        startPointer += 1;
      }
      // a room is free now
      else {
        count -= 1;
        endPointer += 1;
      }
      usedRooms = Math.max(usedRooms, count);
    }

    return usedRooms;
  }
}
```
## Complexity Analysis
```
- Time Complexity:
  - Better approach: O(nlogn)
- Space Complexity:
  - Better approach: O(n)
```
