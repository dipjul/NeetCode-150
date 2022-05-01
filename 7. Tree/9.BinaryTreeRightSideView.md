# 199. Binary Tree Right Side View
Medium


Given the root of a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

 

Example 1:

```
Input: root = [1,2,3,null,5,null,4]
Output: [1,3,4]
```
Example 2:
```
Input: root = [1,null,3]
Output: [1,3]
```
Example 3:
```
Input: root = []
Output: []
 ```

Constraints:

- The number of nodes in the tree is in the range [0, 100].
- -100 <= Node.val <= 100

## Approach
```
- BFS
- Queue
- add the last element of each level into the result list
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
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if(root == null)
            return res;
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        
        while(!queue.isEmpty()) {
            int levelSize = queue.size();
            for(int i = 0; i < levelSize; i++) {
                TreeNode currNode = queue.poll();
                if(currNode.left != null)
                    queue.offer(currNode.left);
                if(currNode.right != null)
                    queue.offer(currNode.right);
                if(i == levelSize-1)
                    res.add(currNode.val);
            }
        }
        
        return res;
    }
}
```

## Complexity Analysis
```
- Time Complexity: O(N)
- Space Complexity: O(N)
```
