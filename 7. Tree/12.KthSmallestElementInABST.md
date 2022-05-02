# 230. Kth Smallest Element in a BST
Medium


Given the root of a binary search tree, and an integer k, return the kth smallest value (1-indexed) of all the values of the nodes in the tree.

 

Example 1:
```
Input: root = [3,1,4,null,2], k = 1
Output: 1
```
Example 2:
```
Input: root = [5,3,6,2,4,null,null,1], k = 3
Output: 3
 ```

Constraints:

- The number of nodes in the tree is n.
- 1 <= k <= n <= 10<sup>4</sup>
- 0 <= Node.val <= 10<sup>4</sup>
 

### Follow up: If the BST is modified often (i.e., we can do insert and delete operations) and you need to find the kth smallest frequently, how would you optimize?

## Approach
```
- Recursion
- inorder traversal gives nodes in sorted order of a BST
- ans[] -> store the answer and k in the second index
- decrement ans[1] until it become 0
  - when it become zero, that node is the ans
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
    public int kthSmallest(TreeNode root, int k) {
        int[] ans = new int[2];
        ans[1] = k;
        inorder(root, ans);
        return ans[0];
    }
    
    private void inorder(TreeNode root, int[] ans) {
        if(root == null)
            return;
        inorder(root.left, ans);
        ans[1]--;
        if(ans[1] == 0)
            ans[0] = root.val;
        inorder(root.right, ans);
    }
}
```

## Complexity Analysis
```
- Time Complexity: O(N)
- Space Complexity: O(N)
```
