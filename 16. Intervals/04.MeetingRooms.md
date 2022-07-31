# 920 · Meeting Rooms [LintCode]
Easy


Description
Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...] (si < ei), determine if a person could attend all meetings.

Wechat reply the【Video】get the free video lessons , the latest frequent Interview questions , etc. (wechat id :jiuzhang15)


> (0,8),(8,10) is not conflict at 8


Example 1
```
Input: intervals = [(0,30),(5,10),(15,20)]
Output: false
Explanation: 
(0,30), (5,10) and (0,30),(15,20) will conflict
```
Example 2
```
Input: intervals = [(5,8),(9,15)]
Output: true
Explanation: 
Two times will not conflict 
```

```java
/**
 * Definition of Interval:
 * public classs Interval {
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
     * @return: if a person could attend all meetings
     */
    public boolean canAttendMeetings(List<Interval> intervals) {

        if(intervals.size() == 0 || intervals.size() == 1)
            return true;
        Collections.sort(intervals, (a,b)->a.end-b.end);
        Interval next = intervals.get(intervals.size()-1);
        for(int i = intervals.size()-2; i >= 0; i--) {
            Interval current = intervals.get(i);

            if(current.end > next.start && current.end <= next.end)
                return false;
            next = current;
        }
        return true;
    }
}

```
