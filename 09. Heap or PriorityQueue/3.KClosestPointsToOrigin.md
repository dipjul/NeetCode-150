# 973. K Closest Points to Origin
Medium


Given an array of points where points[i] = [xi, yi] represents a point on the X-Y plane and an integer k, return the k closest points to the origin (0, 0).

The distance between two points on the X-Y plane is the Euclidean distance (i.e., √(x1 - x2)2 + (y1 - y2)2).

You may return the answer in any order. The answer is guaranteed to be unique (except for the order that it is in).

 

Example 1:
```
Input: points = [[1,3],[-2,2]], k = 1
Output: [[-2,2]]
Explanation:
The distance between (1, 3) and the origin is sqrt(10).
The distance between (-2, 2) and the origin is sqrt(8).
Since sqrt(8) < sqrt(10), (-2, 2) is closer to the origin.
We only want the closest k = 1 points from the origin, so the answer is just [[-2,2]].
```
Example 2:
```
Input: points = [[3,3],[5,-1],[-2,4]], k = 2
Output: [[3,3],[-2,4]]
Explanation: The answer [[-2,4],[3,3]] would also be accepted.
 ```

Constraints:

- 1 <= k <= points.length <= <sup>4</sup>
- -10<sup>4</sup> < xi, yi < <sup>4</sup>

## Approach
```
- Have a Max PriorityQueue based on euclidean distance
- add each point to PQ, if size > k then poll
- remaining points inside the PQ is the answer
```

## Solution
```java
class Solution {
    public int[][] kClosest(int[][] points, int k) {
        int[][] res = new int[k][2];
        PriorityQueue<Point> pq = new PriorityQueue<Point>((a, b) -> new Double(b.dist).compareTo(new Double(a.dist)));
        
        for(int[] point: points) {
            pq.offer(new Point(point[0], point[1]));
            if(pq.size() > k)
                pq.poll();
        }
        int ind = 0;
        while(!pq.isEmpty()) {
            Point p = pq.poll();
            res[ind][0] = p.x;
            res[ind][1] = p.y;
            ind++;
        }
        return res;
    }
}

class Point {
    int x;
    int y;
    
    double dist;
    
    Point(int x, int y) {
        this.x = x;
        this.y = y;
        dist = Math.pow(x*x + y*y, 0.5);
    }
}
```

```java
class Solution {
    public int[][] kClosest(int[][] points, int k) {
        int[][] res = new int[k][2];
        PriorityQueue<int[]> pq = new PriorityQueue<int[]>((a, b) -> (b[0]*b[0] + b[1]*b[1]) - (a[0]*a[0] + a[1]*a[1]));
        
        for(int[] point: points) {
            pq.offer(point);
            if(pq.size() > k)
                pq.poll();
        }
        int ind = 0;
        while(!pq.isEmpty()) {
            int[] p = pq.poll();
            res[ind][0] = p[0];
            res[ind][1] = p[1];
            ind++;
        }
        return res;
    }
}
```

## Complexity Analysis
```
- Time Complexity: O(nlogk) -> Adding to/removing from the heap (or priority queue) 
                            only takes O(\log k) time when the size of the heap is capped at k elements.
- Space Complexity: O(k) -> The heap (or priority queue) will contain at most kk elements.
```

TODO: Quick Select, BinarySearch solution of this problem
