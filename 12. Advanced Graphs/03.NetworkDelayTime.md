# [743. Network Delay Time](https://leetcode.com/problems/network-delay-time/)
Medium


You are given a network of n nodes, labeled from 1 to n. You are also given times, a list of travel times as directed edges times[i] = (ui, vi, wi), where ui is the source node, vi is the target node, and wi is the time it takes for a signal to travel from source to target.

We will send a signal from a given node k. Return the minimum time it takes for all the n nodes to receive the signal. If it is impossible for all the n nodes to receive the signal, return -1.

 

Example 1:
```
Input: times = [[2,1,1],[2,3,1],[3,4,1]], n = 4, k = 2
Output: 2
```
Example 2:
```
Input: times = [[1,2,1]], n = 2, k = 1
Output: 1
```
Example 3:
```
Input: times = [[1,2,1]], n = 2, k = 2
Output: -1
``` 

Constraints:

- 1 <= k <= n <= 100
- 1 <= times.length <= 6000
- times[i].length == 3
- 1 <= ui, vi <= n
- ui != vi
- 0 <= wi <= 100
- All the pairs (ui, vi) are unique. (i.e., no multiple edges.)

## Approach
```

```

## Solution
```java
public class Solution {

    public int networkDelayTime(int[][] times, int n, int k) {
        Map<Integer, List<int[]>> graph = new HashMap<>();
        for (int[] time : times) {
            List<int[]> neighbours = graph.getOrDefault(time[0], new ArrayList<>());
            neighbours.add(new int[] { time[1], time[2] });
            graph.put(time[0], neighbours);
        }
        int[] cost = new int[n + 1];
        for (int i = 1; i <= n; i++) cost[i] = 100005;
        cost[k] = 0;
        Queue<Integer> q = new LinkedList<>();
        q.offer(k);
        while (!q.isEmpty()) {
            int vertex = q.poll();
            if (!graph.containsKey(vertex)) continue;

            List<int[]> neighbours = graph.get(vertex);
            for (int[] nei : neighbours) {
                int newCost = cost[vertex] + nei[1];
                if (newCost < cost[nei[0]]) {
                    cost[nei[0]] = newCost;
                    q.offer(nei[0]);
                }
            }
        }
        int ans = -1;
        for (int i = 1; i <= n; i++) {
            if (cost[i] >= 100005) return -1;
            if (cost[i] > ans) ans = cost[i];
        }
        return ans;
    }
}

```

## Complexity Analysis
```
- Time Complexity:
- Space Complexity:
```
