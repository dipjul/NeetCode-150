# 143. Reorder List
Medium


You are given the head of a singly linked-list. The list can be represented as:

L0 → L1 → … → Ln - 1 → Ln
Reorder the list to be on the following form:

L0 → Ln → L1 → Ln - 1 → L2 → Ln - 2 → …
You may not modify the values in the list's nodes. Only nodes themselves may be changed.

 

Example 1:
```
Input: head = [1,2,3,4]
Output: [1,4,2,3]
```
Example 2:
```
Input: head = [1,2,3,4,5]
Output: [1,5,2,4,3]
 ```

Constraints:

- The number of nodes in the list is in the range [1, 5 * 104].
- 1 <= Node.val <= 1000

## Approach
```
- Reverse the other half(mid to end)
- 2 pointers one from the head other from the reverse head of other list
- use temp variable to keep the next pointers of both the list
- 1st list's next points to 2nd list & 2nd list's next point to the temp variable containing the next of the 1st list
- move both the pointers 
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
    public void reorderList(ListNode head) {
        ListNode slow = head, fast = head.next;
        
        while(fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        ListNode first = head, second = reverse(slow.next);
        slow.next = null;
        
        while(second != null) {
            ListNode tmp1 = first.next, tmp2 = second.next;
            first.next = second;
            second.next = tmp1;
            first = tmp1;
            second = tmp2;
        }
        
        
    }
    
    private ListNode reverse(ListNode head) {
        ListNode curr = head, prev = null, next = null;
        
        while(curr != null) {
            next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }
        return prev;
    }
}
```

## Complexity Analysis
```
- Time Complexity: O(2*N) ~ O(N)
- Space Complexity: O(1)
```
