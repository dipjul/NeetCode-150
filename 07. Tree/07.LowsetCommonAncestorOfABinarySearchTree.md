# 235. Lowest Common Ancestor of a Binary Search Tree
Easy


Given a binary search tree (BST), find the lowest common ancestor (LCA) of two given nodes in the BST.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we allow a node to be a descendant of itself).”

 

Example 1:
```
Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
Output: 6
Explanation: The LCA of nodes 2 and 8 is 6.
```
Example 2:
```
Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 4
Output: 2
Explanation: The LCA of nodes 2 and 4 is 2, since a node can be a descendant of itself according to the LCA definition.
```
Example 3:
``
Input: root = [2,1], p = 2, q = 1
Output: 2
 ``

Constraints:

- The number of nodes in the tree is in the range `[2, 105]`.
- -10<sup>9</sup> <= Node.val <= 10<sup>9</sup>
- All Node.val are unique.
- p != q
- p and q will exist in the BST.

## Approach
```
- Recursion
- if root's val < p's val & q's val then reduce the problem to right subtree of root
- else if root's val > p's val & q's val then reduce the problem to left subtree of root
- else return root (if p's val or q's val equal to root's val or for p & q lies in different subtree of the root)
```

## Solution
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */

class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root == null)
            return null;
        int val = root.val;
        if(val < p.val && val < q.val)
            return lowestCommonAncestor(root.right, p, q);
        else if(val > p.val && val > q.val)
            return lowestCommonAncestor(root.left, p, q);
        return root;
    }
}
```

## Complexity Analysis
```
- Time Complexity: O(logN)
- Space Complexity: O(logN) recursive calls
```
