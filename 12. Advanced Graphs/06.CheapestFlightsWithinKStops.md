# [787. Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops/)
Medium


There are n cities connected by some number of flights. You are given an array flights where flights[i] = [fromi, toi, pricei] indicates that there is a flight from city fromi to city toi with cost pricei.

You are also given three integers src, dst, and k, return the cheapest price from src to dst with at most k stops. If there is no such route, return -1.

 

Example 1:
```
Input: n = 4, flights = [[0,1,100],[1,2,100],[2,0,100],[1,3,600],[2,3,200]], src = 0, dst = 3, k = 1
Output: 700
Explanation:
The graph is shown above.
The optimal path with at most 1 stop from city 0 to 3 is marked in red and has cost 100 + 600 = 700.
Note that the path through cities [0,1,2,3] is cheaper but is invalid because it uses 2 stops.
```
Example 2:
```
Input: n = 3, flights = [[0,1,100],[1,2,100],[0,2,500]], src = 0, dst = 2, k = 1
Output: 200
Explanation:
The graph is shown above.
The optimal path with at most 1 stop from city 0 to 2 is marked in red and has cost 100 + 100 = 200.
```
Example 3:
```
Input: n = 3, flights = [[0,1,100],[1,2,100],[0,2,500]], src = 0, dst = 2, k = 0
Output: 500
Explanation:
The graph is shown above.
The optimal path with no stops from city 0 to 2 is marked in red and has cost 500.
``` 

Constraints:
- 1 <= n <= 100
- 0 <= flights.length <= (n * (n - 1) / 2)
- flights[i].length == 3
- 0 <= fromi, toi < n
- fromi != toi
- 1 <= pricei <= 104
- There will not be any multiple flights between two cities.
- 0 <= src, dst, k < n
- src != dst

## Approach
### Ref: [Bellman Ford](https://github.com/dipjul/NeetCode-150/blob/9a8121cc3db395bc2b180b56c88524c678b72d03/Algorithms/4.Bellman-ford.md)
```
- Bellman ford algorithm
- It runs for n * E time, n : number of nodes & E : edges
- here modified to run for k+1 times
```

## Solution
```java
class Solution {
    
    public int findCheapestPrice(int n, int[][] flights, int src, int dst, int k) {
        int[] cost = new int[n];
        Arrays.fill(cost, Integer.MAX_VALUE);
        int[] tmp = new int[n];
        Arrays.fill(tmp, Integer.MAX_VALUE);
        cost[src] = 0;
        tmp[src] = 0;
        while(k >= 0) {
            for(int[] flight : flights) {
                if(cost[flight[0]] != Integer.MAX_VALUE) {
                    int newCost = cost[flight[0]]+flight[2];
                    if(newCost < tmp[flight[1]])
                        tmp[flight[1]] = newCost;
                }
            }
            cost = Arrays.copyOfRange(tmp, 0, n);
            k--;
        }
        return cost[dst] == Integer.MAX_VALUE?-1:cost[dst];
    }
}
```

## Complexity Analysis
```
- Time Complexity: O(k*E), E size of flights array
- Space Complexity: O(n)
```
