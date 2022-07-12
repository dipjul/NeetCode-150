# 23. Merge k Sorted Lists
Hard


You are given an array of k linked-lists lists, each linked-list is sorted in ascending order.

Merge all the linked-lists into one sorted linked-list and return it.

 

Example 1:
```
Input: lists = [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]
Explanation: The linked-lists are:
[
  1->4->5,
  1->3->4,
  2->6
]
merging them into one sorted list:
1->1->2->3->4->4->5->6
```
Example 2:
```
Input: lists = []
Output: []
```
Example 3:
```
Input: lists = [[]]
Output: []
``` 

Constraints:

- k == lists.length
- 0 <= k <= 104
- 0 <= lists[i].length <= 500
- -10<sup>4</sup> <= lists[i][j] <= 10<sup>4</sup>
- lists[i] is sorted in ascending order.
- The sum of lists[i].length will not exceed 10<sup>4</sup>.

## Approach
```
- Create a function to merge two sorted lists
- Use it to merge all the given lists
Sub approach 1:
  - we can merge two lists then use the merge list as new list and merge it with next given list
Sub approach 2:
  - we can merge all the lists as a group of 2 lists untill we're left with 1 final list
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
    public ListNode mergeKLists(ListNode[] lists) {
        int k = lists.length;
        if(k == 0)
            return null;
        int i = 0;
        while(i+1<k) {
            ListNode l1 = lists[i], l2 = lists[i+1];
            lists[i+1] = merge2LL(l1, l2);
            i++;
        }
        return lists[k-1];
    }
    
    public ListNode merge2LL(ListNode l1, ListNode l2) {
       ListNode dummyHead = new ListNode(0);
       ListNode tmp = dummyHead;
       while(l1 != null && l2 != null) {
           if(l1.val < l2.val) {
                tmp.next = l1;
                ListNode nextL1 = l1.next;
                l1.next = l2;
                l1 = nextL1;
                tmp = tmp.next;
           } else {
                tmp.next = l2;
                ListNode nextL2 = l2.next;
                l2.next = l1;
                l2 = nextL2;
                tmp = tmp.next;
           }
       }

       if(l1 == null)
           tmp.next = l2;
       if(l2 == null)
           tmp.next = l1;
       return dummyHead.next;
   }
}
```
### Optimized
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
    public ListNode mergeKLists(ListNode[] lists) {
        return partion(lists, 0, lists.length - 1);
    }

    public ListNode partion(ListNode[] lists, int s, int e) {
        if (s == e) return lists[s];
        if (s < e) {
            int q = (s + e) / 2;
            ListNode l1 = partion(lists, s, q);
            ListNode l2 = partion(lists, q + 1, e);
            return merge2LL(l1, l2);
        } else return null;
    }

    public ListNode merge2LL(ListNode l1, ListNode l2) {
        ListNode dummyHead = new ListNode(0);
        ListNode tmp = dummyHead;
        while (l1 != null && l2 != null) {
            if (l1.val < l2.val) {
                tmp.next = l1;
                ListNode nextL1 = l1.next;
                l1.next = l2;
                l1 = nextL1;
                tmp = tmp.next;
            } else {
                tmp.next = l2;
                ListNode nextL2 = l2.next;
                l2.next = l1;
                l2 = nextL2;
                tmp = tmp.next;
            }
        }

        if (l1 == null) tmp.next = l2;
        if (l2 == null) tmp.next = l1;
        return dummyHead.next;
    }
}

```

## Complexity Analysis
```
- Time complexity : O(Nlogk) where k is the number of linked lists.
    We can merge two sorted linked list in O(n) time where nn is the total number of nodes in two lists.
    Sum up the merge process and we can get: O(Nlogk)
- Space complexity : O(logk) for recursive call stack
  We can merge two sorted linked lists in O(1) space.
```
