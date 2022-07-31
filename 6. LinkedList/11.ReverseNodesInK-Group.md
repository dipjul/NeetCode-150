# [25. Reverse Nodes in k-Group](https://leetcode.com/problems/reverse-nodes-in-k-group/)
Hard


Given the head of a linked list, reverse the nodes of the list k at a time, and return the modified list.

k is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of k then left-out nodes, in the end, should remain as it is.

You may not alter the values in the list's nodes, only nodes themselves may be changed.

 

Example 1:
```
Input: head = [1,2,3,4,5], k = 2
Output: [2,1,4,3,5]
```
Example 2:
```
Input: head = [1,2,3,4,5], k = 3
Output: [3,2,1,4,5]
 ```

Constraints:
- The number of nodes in the list is n.
- 1 <= k <= n <= 5000
- 0 <= Node.val <= 1000
 

> Follow-up: Can you solve the problem in O(1) extra memory space?

## Approach
```
- Reusing reverse linkedlist function
- dummy root, it's next point to head of given linkedlist
- use two pointer curr and prev
- storing firstNode of every group
- index to find whether we have the complete group or not, as it determines whether we have reverse the that group or not
- if complete group is there prev.next points to the newly reversed list and 
  the prev points to firstNode(prev group, which is the last node of the prev group)
- else prev.next points to firstNode
```

## Solution
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseKGroup(ListNode head, int k) {

        ListNode root = new ListNode(0, head); // dummy head
        ListNode curr = head, prev = root;
        
        while(curr != null) {
            ListNode tail = curr; // keep track of the 1st element of each group
            int listIndex = 0;
            
            while(curr != null && listIndex < k) {
                curr = curr.next;
                listIndex++;
            }
            // listIndex != k means we have a group less than k size
            if(listIndex != k)
                prev.next = tail;
                // less than k size so simply pointing prev to the 
                // first element of the group
            else {
                // reverse the group
                prev.next = reverse(tail, k);
                // prev will move to the first element(now the last) of the group
                // so that next of it would have the reverse of the group
                prev = tail;
            }
        }
        return root.next;
    }
    
    private ListNode reverse(ListNode head, int k) {
        ListNode curr = head, prev = null, next = null;
        
        while(curr != null && k > 0) {
            k--;
            next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }
        head = prev;
        return head;
    }
}
```

## Complexity Analysis
```
- Time Complexity: O(n)
- Space Complexity: O(1)
```
