# 102. Binary Tree Level Order Traversal
Medium


Given the root of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).

 

Example 1:

```
Input: root = [3,9,20,null,null,15,7]
Output: [[3],[9,20],[15,7]]
```
Example 2:
```
Input: root = [1]
Output: [[1]]
```
Example 3:
```
Input: root = []
Output: []
``` 

Constraints:

- The number of nodes in the tree is in the range [0, 2000].
- -1000 <= Node.val <= 1000

## Approach
```
- Use Queue to insert the nodes
- for each level we'll poll node and check if left or right of it is not null then add left or right of it to the queue
```

## Solution
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        if(root == null)
            return result;
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        
        while(!queue.isEmpty()) {
            int levelSize = queue.size();
            List<Integer> currLevel = new ArrayList<>(levelSize);
            
            for(int i = 0; i < levelSize; i++) {
                TreeNode currNode = queue.poll();
                currLevel.add(currNode.val);
                if(currNode.left != null)
                    queue.offer(currNode.left);
                if(currNode.right != null)
                    queue.offer(currNode.right);
            }
            
            result.add(currLevel);
        }
        return result;
    }
}
```

## Complexity Analysis
```
- Time Complexity: O(N)
- Space Complexity: O(N), max number of nodes in a level
```
