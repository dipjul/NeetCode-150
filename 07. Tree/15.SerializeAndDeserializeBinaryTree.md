[297. Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)

Hard


Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

Clarification: The input/output format is the same as how LeetCode serializes a binary tree. You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

 

Example 1:
```
Input: root = [1,2,3,null,null,4,5]
Output: [1,2,3,null,null,4,5]
```
Example 2:
```
Input: root = []
Output: []
``` 

Constraints:

- The number of nodes in the tree is in the range [0, 104].
- -1000 <= Node.val <= 1000

## Approach
```

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
public class Codec {

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        StringBuilder result = new StringBuilder();
        serialHelper(root, result);
        return result.toString();
    }

    private void serialHelper(TreeNode root, StringBuilder result) {
        if (root == null) {
            return;
        }
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        while (!q.isEmpty()) {
            TreeNode curr = q.poll();
            if (curr == null) {
                result.append(",");
                continue;
            }
            result.append(curr.val + ",");
            q.offer(curr.left);
            q.offer(curr.right);
        }
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        String[] nodes = data.split(",");

        if (nodes[0] == "") return null;
        return deserialHelper(nodes);
    }

    private TreeNode deserialHelper(String[] data) {
        String val = data[0];
        TreeNode root = new TreeNode(Integer.parseInt(val));
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        for (int i = 1; i < data.length; i += 2) {
            TreeNode curr = q.poll();
            if (!data[i].equals("")) {
                curr.left = new TreeNode(Integer.parseInt(data[i]));
                q.offer(curr.left);
            }
            if (i + 1 < data.length && !data[i + 1].equals("")) {
                curr.right = new TreeNode(Integer.parseInt(data[i + 1]));
                q.offer(curr.right);
            }
        }

        return root;
    }
}
// Your Codec object will be instantiated and called as such:
// Codec ser = new Codec();
// Codec deser = new Codec();
// TreeNode ans = deser.deserialize(ser.serialize(root));
```

## Complexity Analysis
```
- Time Complexity: O(N)
- Space Complexity: O(N)
```
