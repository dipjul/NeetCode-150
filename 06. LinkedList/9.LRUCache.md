# 146. LRU Cache
Medium


Design a data structure that follows the constraints of a Least Recently Used (LRU) cache.

Implement the LRUCache class:
- `LRUCache(int capacity)` Initialize the LRU cache with positive size capacity.
- `int get(int key)` Return the value of the key if the key exists, otherwise return -1.
- `void put(int key, int value)` Update the value of the key if the key exists. Otherwise, add the key-value pair to the cache. If the number of keys exceeds the capacity from this operation, evict the least recently used key.
- The functions get and put must each run in O(1) average time complexity.

 

Example 1:
```
Input
["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
Output
[null, null, null, 1, null, -1, null, -1, 3, 4]

Explanation
LRUCache lRUCache = new LRUCache(2);
lRUCache.put(1, 1); // cache is {1=1}
lRUCache.put(2, 2); // cache is {1=1, 2=2}
lRUCache.get(1);    // return 1
lRUCache.put(3, 3); // LRU key was 2, evicts key 2, cache is {1=1, 3=3}
lRUCache.get(2);    // returns -1 (not found)
lRUCache.put(4, 4); // LRU key was 1, evicts key 1, cache is {4=4, 3=3}
lRUCache.get(1);    // return -1 (not found)
lRUCache.get(3);    // return 3
lRUCache.get(4);    // return 4
 ```

Constraints:

- 1 <= capacity <= 3000
- 0 <= key <= 10<sup>4</sup>
- 0 <= value <= 10<sup>5</sup>
- At most 2 * 10<sup>5</sup> calls will be made to get and put.

## Approach
```
- Doublely linkedlist, it allows O(1) deletion of a given node
- Map to keep the key mapped to a node, getting the value for a key at O(1) time
- Keeping head and tail of the linked list
- add at head and remove from tail(if size exceeds)
- get method:
  - if map doesn't contain the key return -1
  - else get the node, remove it, add it (it'll add it to the head of the list), return the value
  
- put method:
  - if map already contains the key, remove the node
  - size of map = size, then remove the node at tail
  - insert the new node
  
- insert method: (helper method)
  - add the node to the next of the head and update the pointers
  - add the key and node to the map
  
- remove method: (helper method)
  - remove the node using the pointers
  - remove the key and node from the map

```

## Solution
```java
/* 
* Hepler class
* Node to create doublely linked list
*/
class Node {
    int key;
    int val;
    Node prev;
    Node next;
    Node(int key, int val) {
        this.key = key;
        this.val = val;
    }
}

class LRUCache {
    Node head = new Node(0, 0);
    Node tail = new Node(0, 0);
    Map<Integer, Node> mp;
    int size;
    
    public LRUCache(int capacity) {
        head.next = tail;
        tail.prev = head;
        mp = new HashMap<>();
        size = capacity;
    }
    
    public int get(int key) {
        if(mp.containsKey(key)) {
            Node node = mp.get(key);
            remove(node);
            insert(node);
            return node.val;
        } else
            return -1;
    }
    
    public void put(int key, int value) {
        if(mp.containsKey(key)) {
            Node node = mp.get(key);
            remove(node);
        }
        if(mp.size() == size)
            remove(tail.prev);
        insert(new Node(key, value));
    }
    
    private void remove(Node node) {
        mp.remove(node.key);
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }
    
    private void insert(Node node) {
        Node headNext = head.next;
        head.next = node;
        node.prev = head;
        node.next = headNext;
        headNext.prev = node;
        mp.put(node.key, node);
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```

## Complexity Analysis
```
- Time Complexity: (on average)
  - get() : O(1)
  - put() : O(1)
  
- Space Complexity:
  - ~ O(N) for map and doublely linkedlist (over all)
  - get() : O(1)
  - put() : O(1)
```
