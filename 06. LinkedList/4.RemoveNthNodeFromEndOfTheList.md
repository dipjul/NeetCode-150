# 19. Remove Nth Node From End of List
Medium


Given the head of a linked list, remove the nth node from the end of the list and return its head.

 

Example 1:
```
Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]
```
Example 2:
```
Input: head = [1], n = 1
Output: []
```
Example 3:
```
Input: head = [1,2], n = 1
Output: [1]
 ```

Constraints:

The number of nodes in the list is sz.
- 1 <= sz <= 30
- 0 <= Node.val <= 100
- 1 <= n <= sz
 

### Follow up: Could you do this in one pass?

## Approach
```
- 2 pointers approach
- dummy head for so that removing head would be easier 
- fast pointer would be ahead by n nodes
- slow and fast will start moving until fast reach the last element
- slow's next node would be the one we need to remove
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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummyHead = new ListNode(0);
        dummyHead.next = head;
        ListNode slow = dummyHead, fast = dummyHead;
        
        while(n > 0) {
            fast = fast.next;
            n--;
        }
        
        while(fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next;
        }
        
        slow.next = slow.next.next;
        
        return dummyHead.next;
    }
}
```

## Complexity Analysis
```
- Time Complexity: O(N) , one pass only
- Space Complexity: O(1)
```
