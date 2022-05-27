# [846. Hand of Straights](https://leetcode.com/problems/hand-of-straights/)
Medium


Alice has some number of cards and she wants to rearrange the cards into groups so that each group is of size groupSize, and consists of groupSize consecutive cards.

Given an integer array hand where hand[i] is the value written on the ith card and an integer groupSize, return true if she can rearrange the cards, or false otherwise.

 

Example 1:
```
Input: hand = [1,2,3,6,2,3,4,7,8], groupSize = 3
Output: true
Explanation: Alice's hand can be rearranged as [1,2,3],[2,3,4],[6,7,8]
```
Example 2:
```
Input: hand = [1,2,3,4,5], groupSize = 4
Output: false
Explanation: Alice's hand can not be rearranged into groups of 4.
```
 

Constraints:

- 1 <= hand.length <= 104
- 0 <= hand[i] <= 109
- 1 <= groupSize <= hand.length
 

> Note: This question is the same as 1296: https://leetcode.com/problems/divide-array-in-sets-of-k-consecutive-numbers/

## Approach
```
// TODO
```

## Solution
```java
class Solution {
    public boolean isNStraightHand(int[] hand, int groupSize) {
        if(hand.length % groupSize != 0)
            return false;
        
        
        Map<Integer, Integer> mp = new HashMap<>();
        PriorityQueue<Integer> pq = new PriorityQueue<>((a,b)->a-b);
        
        for(int i = 0; i < hand.length; i++) {
           if(!mp.containsKey(hand[i])) {
               pq.offer(hand[i]);
               mp.put(hand[i], 1);
           } else {
               mp.put(hand[i], mp.get(hand[i])+1);
           }
        }
        
        while(!pq.isEmpty()) {
            int min = pq.peek();
            int sz  = 0;
            while(sz < groupSize) {
                if(!mp.containsKey(min))
                    return false;
                mp.put(min, mp.get(min)-1);
                if(mp.get(min) == 0) {
                    mp.remove(min);
                    int val = pq.poll();
                    if(val != min)
                        return false;
                }
                min++;
                sz++;
            }

        }
        return true;
    }
}

```

## Complexity Analysis
```
- Time Complexity: 
- Space Complexity: 
```
