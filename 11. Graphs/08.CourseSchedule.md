# [207. Course Schedule](https://leetcode.com/problems/course-schedule/)
Medium


There are a total of numCourses courses you have to take, labeled from 0 to numCourses - 1. You are given an array prerequisites where prerequisites[i] = [ai, bi] indicates that you must take course bi first if you want to take course ai.

For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1.
Return true if you can finish all courses. Otherwise, return false.

 

Example 1:
```
Input: numCourses = 2, prerequisites = [[1,0]]
Output: true
Explanation: There are a total of 2 courses to take. 
To take course 1 you should have finished course 0. So it is possible.
```
Example 2:
```
Input: numCourses = 2, prerequisites = [[1,0],[0,1]]
Output: false
Explanation: There are a total of 2 courses to take. 
To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.
``` 

Constraints:

- 1 <= numCourses <= 2000
- 0 <= prerequisites.length <= 5000
- prerequisites[i].length == 2
- 0 <= ai, bi < numCourses
- All the pairs prerequisites[i] are unique.

## Approach
```
Topological Sort
- Have look a the solution for understanding the Topological sort algorithm
```

## Solution
```java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        // List<Integer> result = new ArrayList<>();
        int result = 0;
        
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
            result++;
            for(int child:graph.get(vertex)) {
                inDegree.put(child, inDegree.get(child)-1);
                if(inDegree.get(child) == 0)
                    sources.offer(child);
            }
        }
        
        // 5. If size of result equal to numCourses then return true else return false
        return result == numCourses;
    }
}
```

## Complexity Analysis
```
- Time Complexity: O(m*n)
- Space Complexity: O(m*n)
```
