# [210. Course Schedule II](https://leetcode.com/problems/course-schedule-ii/)
Medium


There are a total of numCourses courses you have to take, labeled from 0 to numCourses - 1. You are given an array prerequisites where prerequisites[i] = [ai, bi] indicates that you must take course bi first if you want to take course ai.

For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1.
Return the ordering of courses you should take to finish all courses. If there are many valid answers, return any of them. If it is impossible to finish all courses, return an empty array.

 

Example 1:
```
Input: numCourses = 2, prerequisites = [[1,0]]
Output: [0,1]
Explanation: There are a total of 2 courses to take. To take course 1 you should have finished course 0. So the correct course order is [0,1].
```
Example 2:
```
Input: numCourses = 4, prerequisites = [[1,0],[2,0],[3,1],[3,2]]
Output: [0,2,1,3]
Explanation: There are a total of 4 courses to take. To take course 3 you should have finished both courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0.
So one correct course order is [0,1,2,3]. Another correct ordering is [0,2,1,3].
```
Example 3:
```
Input: numCourses = 1, prerequisites = []
Output: [0]
 ```

Constraints:

- 1 <= numCourses <= 2000
- 0 <= prerequisites.length <= numCourses * (numCourses - 1)
- prerequisites[i].length == 2
- 0 <= ai, bi < numCourses
- ai != bi
- All the pairs [ai, bi] are distinct.

## Aprroach
Ref: [8. Course Schedule](https://github.com/dipjul/NeetCode-150/blob/1db1597fe0d82d4741ecd5ee3600aea518824bb1/11.%20Graphs/8.CourseSchedule.md)
```
Topologicalo Sort
```

## Solution
```java
class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        List<Integer> result = new ArrayList<>();
        
        // 1. Initialize the graph
        Map<Integer, List<Integer>> graph = new HashMap<>();
        Map<Integer, Integer> inDegree = new HashMap<>();
        
        for(int i = 0; i < numCourses; i++) {
            graph.put(i, new ArrayList<>());
            inDegree.put(i, 0);
        }
        
        // 2. Build the graph
        for(int i = 0; i < prerequisites.length; i++) {
            int child = prerequisites[i][0], parent = prerequisites[i][1];
            graph.get(parent).add(child);
            inDegree.put(child, inDegree.get(child)+1);
        }
        
        // 3. Add all the sources(i.e, vertices with in-degree 0) to a queue
        Queue<Integer> sources = new LinkedList<>();
        for(Map.Entry<Integer, Integer> entry: inDegree.entrySet())
            if(entry.getValue() == 0)
                sources.offer(entry.getKey());
        
        // 4. For each source, add it to the result, subtract 1 from all of it's children's in-degree
        // & add if any child has in-degree 0, add it to sources queue
        while(!sources.isEmpty()) {
            int vertex = sources.poll();
            result.add(vertex);
            for(int child:graph.get(vertex)) {
                inDegree.put(child, inDegree.get(child)-1);
                if(inDegree.get(child) == 0)
                    sources.offer(child);
            }
        }
        
        if(result.size() != numCourses)
            return new int[]{};
        return result.stream().mapToInt(i->i).toArray();
    }
}
```

## Complexity Analysis
```
- Time Complexity: O(n*m)
- Space Complexity: O(n*m)
```
