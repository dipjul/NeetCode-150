# [621. Task Scheduler](https://leetcode.com/problems/task-scheduler/)
Medium


Given a characters array tasks, representing the tasks a CPU needs to do, where each letter represents a different task. Tasks could be done in any order. Each task is done in one unit of time. For each unit of time, the CPU could complete either one task or just be idle.

However, there is a non-negative integer n that represents the cooldown period between two same tasks (the same letter in the array), that is that there must be at least n units of time between any two same tasks.

Return the least number of units of times that the CPU will take to finish all the given tasks.

 

Example 1:
```
Input: tasks = ["A","A","A","B","B","B"], n = 2
Output: 8
Explanation: 
A -> B -> idle -> A -> B -> idle -> A -> B
There is at least 2 units of time between any two same tasks.
```
Example 2:
```
Input: tasks = ["A","A","A","B","B","B"], n = 0
Output: 6
Explanation: On this case any permutation of size 6 would work since n = 0.
["A","A","A","B","B","B"]
["A","B","A","B","A","B"]
["B","B","B","A","A","A"]
...
And so on.
```
Example 3:
```
Input: tasks = ["A","A","A","A","A","A","B","C","D","E","F","G"], n = 2
Output: 16
Explanation: 
One possible solution is
A -> B -> C -> A -> D -> E -> A -> F -> G -> A -> idle -> idle -> A -> idle -> idle -> A
 ```

Constraints:

- 1 <= task.length <= 104
- tasks[i] is upper-case English letter.
- The integer n is in the range [0, 100].

## Approach
```

```

## Solution
```java
class Solution {
    public int leastInterval(char[] tasks, int n) {
        int[] freq = new int[26];
        int max = 0; // keep the max value
        int maxCount = 0; // number of tasks with the max value
        
        for(char task : tasks) {
            freq[task-'A']++;
            if(freq[task-'A'] == max) {
                maxCount++;
            } else if(freq[task-'A'] > max) {
                max = freq[task-'A'];
                maxCount = 1;
            }
        }
        
        // number of blank sequence
        int blankSeq = max - 1;
        // number of blanks in each sequence
        int blankSeqLen = n - (maxCount - 1);
        // total empty slots
        int emptySlots = blankSeq * blankSeqLen;
        // non-max tasks count
        int availableSlots = tasks.length - (maxCount * max);
        // total amount of idle tiem
        int idleTime = Math.max(0, emptySlots - availableSlots);
        
        return tasks.length + idleTime;
    }
}

```

## Complexity Analysis
```
- Time Complexity: O(N)
- Space Complexity: O(26)
```
