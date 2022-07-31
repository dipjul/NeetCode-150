# 104. Maximum Depth of Binary Tree

Given the root of a binary tree, return its maximum depth.

A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

```
Example 1:
Input: root = [3,9,20,null,null,15,7]
Output: 3
```
```
Example 2:
Input: root = [1,null,2]
Output: 2
```

Constraints:
- The number of nodes in the tree is in the range [0, 104].
- -100 <= Node.val <= 100

## Approach
```
- Recursion
- if node = null return 0
- return 1 + max(leftHeight, rightHeight)
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
    public int maxDepth(TreeNode root) {
        if(root == null)
            return 0;
        return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
    }
}
```

## Complexity Analysis
```
- Time Complexity: O(N)
- Space Complexity: O(H), height of the tree
```
