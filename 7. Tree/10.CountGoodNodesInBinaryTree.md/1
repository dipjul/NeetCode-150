# [1448. Count Good Nodes in Binary Tree](https://leetcode.com/problems/count-good-nodes-in-binary-tree/)
Medium

Share
Given a binary tree root, a node X in the tree is named good if in the path from root to X there are no nodes with a value greater than X.

Return the number of good nodes in the binary tree.

 

Example 1:
```
Input: root = [3,1,4,3,null,1,5]
Output: 4
Explanation: Nodes in blue are good.
Root Node (3) is always a good node.
Node 4 -> (3,4) is the maximum value in the path starting from the root.
Node 5 -> (3,4,5) is the maximum value in the path
Node 3 -> (3,1,3) is the maximum value in the path.
```
Example 2:
```
Input: root = [3,3,null,4,2]
Output: 3
Explanation: Node 2 -> (3, 3, 2) is not good, because "3" is higher than it.
```
Example 3:
```
Input: root = [1]
Output: 1
Explanation: Root is considered as good.
```

Constraints:
- The number of nodes in the binary tree is in the range [1, 10^5].
- Each node's value is between [-10^4, 10^4].

## Approach
![image](https://user-images.githubusercontent.com/20329508/177685705-372a0dab-a82d-4e81-ba66-681134d12bdc.png)

```
- check if the node is null
- if node.val >= previously send max, res will be one
- res += left Subtree call with updated max
- res += right Subtree call with updated max
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
    public int goodNodes(TreeNode root) {
        return goodNodes(root, Integer.MIN_VALUE);
    }

    public int goodNodes(TreeNode root, int max) {
        if (root == null) return 0;
        int res = root.val >= max ? 1 : 0;
        res += goodNodes(root.left, Math.max(max, root.val));
        res += goodNodes(root.right, Math.max(max, root.val));
        return res;
    }
}
```

## Complexity Analysis
```
- Time Complexity: O(N)
- Space Complexity: O(height)
```
