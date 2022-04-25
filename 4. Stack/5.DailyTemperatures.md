# 739. Daily Temperatures
Medium


Given an array of integers temperatures represents the daily temperatures, return an array answer such that answer[i] is the number of days you have to wait after the ith day to get a warmer temperature. If there is no future day for which this is possible, keep answer[i] == 0 instead.

 

Example 1:
```
Input: temperatures = [73,74,75,71,69,72,76,73]
Output: [1,1,4,2,1,1,0,0]
```
Example 2:
```
Input: temperatures = [30,40,50,60]
Output: [1,1,1,0]
```
Example 3:
```
Input: temperatures = [30,60,90]
Output: [1,1,0]
 ```

Constraints:

- 1 <= temperatures.length <= 10<sup>5</sup>
- 30 <= temperatures[i] <= 100

## Approach
```
- Use a stack to keep temperatures and indices
- We'll check while peek element is less the current temperature
  - We'll pop and res[popped Index] = i-popped Index;
- push each element and index to the stack
```
## TODO: O(1) extra-space
## Solution
```java
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        int n = temperatures.length;
        Stack<int[]> st = new Stack<>();
        int[] res = new int[n];
        
        for(int i = 0; i < n; i++) {
            while(!st.empty() && st.peek()[0] < temperatures[i]) {
                int[] temp = st.pop();
                res[temp[1]] = i-temp[1];
            }
            st.push(new int[]{temperatures[i], i});
        }
        
        return res;
    }
}

```

## Complexity Analysis
```
- Time Complexity: O(N)
  At first glance, it may look like the time complexity of this algorithm should be O(N^2), 
  because there is a nested while loop inside the for loop. However, each element can only be added to the stack once,
  which means the stack is limited to N pops. Every iteration of the while loop uses 1 pop, 
  which means the while loop will not iterate more than N times in total, across all iterations of the for loop.
  An easier way to think about this is that in the worst case, every element will be pushed and popped once. 
  This gives a time complexity of O(2*N) = O(N).
- Space Complexity: O(N)
  If the input was non-increasing, then no element would ever be popped from the stack, 
  and the stack would grow to a size of N elements at the end.
```
