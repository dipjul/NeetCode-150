# [1584. Min Cost to Connect All Points](https://leetcode.com/problems/min-cost-to-connect-all-points/)
Medium


You are given an array points representing integer coordinates of some points on a 2D-plane, where points[i] = [xi, yi].

The cost of connecting two points [xi, yi] and [xj, yj] is the manhattan distance between them: |xi - xj| + |yi - yj|, where |val| denotes the absolute value of val.

Return the minimum cost to make all points connected. All points are connected if there is exactly one simple path between any two points.

 

Example 1:
```
Input: points = [[0,0],[2,2],[3,10],[5,2],[7,0]]
Output: 20
Explanation: 

We can connect the points as shown above to get the minimum cost of 20.
Notice that there is a unique path between every pair of points.
```
Example 2:
```
Input: points = [[3,12],[-2,5],[-4,1]]
Output: 18
 ```

Constraints:

1 <= points.length <= 1000
-106 <= xi, yi <= 106
All pairs (xi, yi) are distinct.

## Approach
```
- MST
- PRIMS Algorithm
```
## Solution
```java
class Solution {
    class Edge {
            int[] x;
            int[] y;
            int cost;
            Edge(int[] x, int[] y) {
                this.x = x;
                this.y = y;
                this.cost = Math.abs(x[0]-y[0])+Math.abs(x[1]-y[1]);
            }
        }


        public int minCostConnectPoints(int[][] points) {
            // MST
            // prims
            int cost = 0;
            Set<int[]> visited = new HashSet<>(); // to store the visited vertices
            int numOfVertices = points.length;
            PriorityQueue<Edge> q = new PriorityQueue<>((a, b)->a.cost-b.cost); // to store the edges based on cost
            visited.add(points[0]);
            Queue<int[]> source = new LinkedList<>(); // sources to determine which node to relax
            source.add(points[0]);
            while(visited.size() != numOfVertices) { // till all nodes are visited or n-1 edges are added
                int[] src = source.poll();
                putEdges(src, visited, points, q); // put hte edges to the queue
                while(!q.isEmpty()) {
                    Edge edge = q.poll(); // get the best edge
                    if (!detectCycle(src, edge.y, visited)) { // if cycle is not form after adding the edge
                        cost += edge.cost;
                        visited.add(edge.y);
                        source.add(edge.y);
                        break; // so that it doesn't look to add the other edges right away
                    }
                }
            }
            return cost;
        }

        private void putEdges(int[] point, Set<int[]> set, int[][] points, PriorityQueue<Edge> q) {
            for(int[] pnt : points) {
                if(pnt != point && !set.contains(pnt))
                    q.offer(new Edge(point, pnt));
            }
        }

        // to detect cycle
        private boolean detectCycle(int[] a, int[] b, Set<int[]> set) {
            return set.contains(a) && set.contains(b);
        }
    }
```
## Complexity Analysis
```
- Time Complexity: O(V*E)
- Space Complexity: O(V+E)
```
