# [124. Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/)
Hard


A path in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence at most once. Note that the path does not need to pass through the root.

The path sum of a path is the sum of the node's values in the path.

Given the root of a binary tree, return the maximum path sum of any non-empty path.

 

Example 1:
```
Input: root = [1,2,3]
Output: 6
Explanation: The optimal path is 2 -> 1 -> 3 with a path sum of 2 + 1 + 3 = 6.
```
Example 2:
```
Input: root = [-10,9,20,null,null,15,7]
Output: 42
Explanation: The optimal path is 15 -> 20 -> 7 with a path sum of 15 + 20 + 7 = 42.
 ```

Constraints:
- The number of nodes in the tree is in the range [1, 3 * 104].
- -1000 <= Node.val <= 1000

## Approach
```
- compare max at each node
- left call, right call
- compare max with node's val+left val, node's val+right val, node's val+left val+right val
- return max of node's val, node's val+left val, node's val+right val
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
    int max;
    public int maxPathSum(TreeNode root) {
        max = -1001;
        helper(root);
        return max;
    }
    
    private int helper(TreeNode root) {
        if(root == null)
            return 0;
        int val = root.val;
        max = Math.max(max, val);
        int lVal = helper(root.left);
        int rVal = helper(root.right);
        max = Math.max(max, Math.max(rVal+val, Math.max(lVal+val, lVal+rVal+val)));
        
        return Math.max(rVal+val, Math.max(lVal+val, val));
    }
}
```
## Complexity Analysis
```
- Time Complexity: O(n)
- Space Complexity: O(logn), recursive call stacks
```
