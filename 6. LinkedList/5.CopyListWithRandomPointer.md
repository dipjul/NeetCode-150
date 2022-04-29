# 138. Copy List with Random Pointer
Medium


A linked list of length n is given such that each node contains an additional random pointer, which could point to any node in the list, or null.

Construct a deep copy of the list. The deep copy should consist of exactly n brand new nodes, where each new node has its value set to the value of its corresponding original node. Both the next and random pointer of the new nodes should point to new nodes in the copied list such that the pointers in the original list and copied list represent the same list state. None of the pointers in the new list should point to nodes in the original list.

For example, if there are two nodes X and Y in the original list, where X.random --> Y, then for the corresponding two nodes x and y in the copied list, x.random --> y.

Return the head of the copied linked list.

The linked list is represented in the input/output as a list of n nodes. Each node is represented as a pair of `[val, random_index]` where:

- `val: an integer representing Node.val`
- `random_index: the index of the node (range from 0 to n-1) that the random pointer points to, or null if it does not point to any node.`

Your code will only be given the head of the original linked list.

 

Example 1:
```
Input: head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
Output: [[7,null],[13,0],[11,4],[10,2],[1,0]]
```
Example 2:
```
Input: head = [[1,1],[2,1]]
Output: [[1,1],[2,1]]
```
Example 3:
```
Input: head = [[3,null],[3,0],[3,null]]
Output: [[3,null],[3,0],[3,null]]
 ```

Constraints:

- 0 <= n <= 1000
- -10<sup>4</sup> <= Node.val <= 10<sup>4</sup>
- `Node.random` is null or is pointing to some node in the linked list.

## Approach
```
- Step 1: Duplicate each node such that old1->new1->old2->new2 ...
- Step 2: Random pointer of new = Random pointer of old's next
- Step 3: Seperate the the nodes to form old1->old2.. & new1->new2..
```

## Solution
```java
/*
// Definition for a Node.
class Node {
    int val;
    Node next;
    Node random;

    public Node(int val) {
        this.val = val;
        this.next = null;
        this.random = null;
    }
}
*/

class Solution {
    public Node copyRandomList(Node head) {
        if(head == null)
            return null;
      
        // Step 1: Duplicate each node such that old1->new1->old2->new2 ...
        Node curr = head, next = null;
        while(curr != null) {
            next = curr.next;
            Node newNode = new Node(curr.val);
            curr.next = newNode;
            newNode.next = next;
            curr = next;
        }
      
         // Step 2: Random pointer of new = Random pointer of old's next
        curr = head;
        Node nextNode = head.next;
        while(nextNode != null) {
            nextNode.random = curr.random == null ? null : curr.random.next;
            if(nextNode.next == null)
                break;
            nextNode = nextNode.next.next;
            curr = curr.next.next;
        }
      
        // Step 3: Seperate the the nodes to form old1->old2.. & new1->new2..
        Node  p = head, c = head.next, n = null;
        Node newListHead = c;
        while(p != null) {
            n = c.next;
            p.next = n;
            if (n == null)
                break;
            c.next = n.next;
            p = p.next;
            c = c.next;
        }

        return newListHead;
    }
}
```

## Complexity Analysis
```
- Time Complexity: O(N+2*N+N) ~ O(N)
- Space Complexity: O(1), no extra memory is used (memory used is for new list only)
```
