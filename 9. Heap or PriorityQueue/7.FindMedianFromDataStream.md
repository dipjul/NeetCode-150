# 295. Find Median from Data Stream
Hard


The median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value and the median is the mean of the two middle values.

For example, for arr = [2,3,4], the median is 3.
For example, for arr = [2,3], the median is (2 + 3) / 2 = 2.5.
Implement the MedianFinder class:

MedianFinder() initializes the MedianFinder object.
void addNum(int num) adds the integer num from the data stream to the data structure.
double findMedian() returns the median of all elements so far. Answers within 10-5 of the actual answer will be accepted.
 

Example 1:
```
Input
["MedianFinder", "addNum", "addNum", "findMedian", "addNum", "findMedian"]
[[], [1], [2], [], [3], []]
Output
[null, null, null, 1.5, null, 2.0]

Explanation
MedianFinder medianFinder = new MedianFinder();
medianFinder.addNum(1);    // arr = [1]
medianFinder.addNum(2);    // arr = [1, 2]
medianFinder.findMedian(); // return 1.5 (i.e., (1 + 2) / 2)
medianFinder.addNum(3);    // arr[1, 2, 3]
medianFinder.findMedian(); // return 2.0
 ```

Constraints:

- -10<sup>5</sup> <= num <= 10<sup>5</sup>
- There will be at least one element in the data structure before calling findMedian.
- At most 5 * 104 calls will be made to addNum and findMedian.
 

Follow up:

- If all integer numbers from the stream are in the range [0, 100], how would you optimize your solution?
- If 99% of all integer numbers from the stream are in the range [0, 100], how would you optimize your solution?

## Approach
```
- Use two heaps, one max heap(smallerList), other min heap(largerList)
- if smallList is not empty and first element is less than equal to num then add num to largeList
- else add num to smallList
- balance the size of both the heaps
  - so that smallList never become more than 1 + size of largeList
  - largeList's size always remain less or equal to the size of smallList
```

## Solution
```java
class MedianFinder {
    int size;
    PriorityQueue<Integer> smallList;
    PriorityQueue<Integer> largeList;
    public MedianFinder() {
        smallList = new PriorityQueue<>(Collections.reverseOrder()); // maxHeap
        largeList = new PriorityQueue<>(); // minHeap
    }
    
    public void addNum(int num) {
        
        if(!smallList.isEmpty() && smallList.peek() <= num)
            largeList.offer(num);
        else
            smallList.offer(num);
        // size balance
        if(smallList.size() > largeList.size()+1) {
            int tmp = smallList.poll();
            largeList.offer(tmp);
        } else if(smallList.size() < largeList.size()) {
            int tmp = largeList.poll();
            smallList.offer(tmp);
        }
        size++;
    }
    
    public double findMedian() {

        if(size % 2 != 0) {
            return (double) smallList.peek();
        } else {
            return (double) (smallList.peek() + largeList.peek())/2.0;
        }
    }
}

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder obj = new MedianFinder();
 * obj.addNum(num);
 * double param_2 = obj.findMedian();
 */
```

## Complexity Analysis
```
- Time Complexity: 
  - add operation: O(logN)
  - find median operation: O(1)
- Space Complexity:
  - add operation: O(1)
  - find median operation: O(1)
```
