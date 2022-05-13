# [208. Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree/)
Medium


A trie (pronounced as "try") or prefix tree is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. There are various applications of this data structure, such as autocomplete and spellchecker.

Implement the Trie class:

- `Trie()` Initializes the trie object.
- `void insert(String word)` Inserts the string word into the trie.
- `boolean search(String word)` Returns true if the string word is in the trie (i.e., was inserted before), and false otherwise.
- `boolean startsWith(String prefix)` Returns true if there is a previously inserted string word that has the prefix prefix, and false otherwise.
 

Example 1:
```
Input
["Trie", "insert", "search", "search", "startsWith", "insert", "search"]
[[], ["apple"], ["apple"], ["app"], ["app"], ["app"], ["app"]]
Output
[null, null, true, false, true, null, true]

Explanation
Trie trie = new Trie();
trie.insert("apple");
trie.search("apple");   // return True
trie.search("app");     // return False
trie.startsWith("app"); // return True
trie.insert("app");
trie.search("app");     // return True
``` 

Constraints:

- 1 <= word.length, prefix.length <= 2000
- word and prefix consist only of lowercase English letters.
- At most 3 * 10<sup>4</sup> calls in total will be made to insert, search, and startsWith.

## Approach
```
 26 links, end marker
 [          ,          , ...26]
 / . . . 26 \ /..26..\
 
```
## Solution
```java
class Trie {
    TrieNode root;
    public Trie() {
        root = new TrieNode();
    }
    
    public void insert(String word) {
        TrieNode curr  = root;
        for(int i = 0; i < word.length(); i++) {
            int ind = word.charAt(i)-'a';
            
            if(curr.node[ind] != null) {
                curr = curr.node[ind];
            } else {
                curr.node[ind] = new TrieNode();
                curr = curr.node[ind];
            }
        }
        curr.end = true;
    }
    
    public boolean search(String word) {
        TrieNode curr = root;
        for(int i = 0; i < word.length(); i++) {
            int ind = word.charAt(i)-'a';
            if(curr.node[ind] != null)
                curr = curr.node[ind];
            else
                return false;
        }
        return curr.end == true;
    }
    
    public boolean startsWith(String prefix) {
        TrieNode curr = root;
        for(int i = 0; i < prefix.length(); i++) {
            int ind = prefix.charAt(i)-'a';
            if(curr.node[ind] != null)
                curr = curr.node[ind];
            else
                return false;
        }
        return true;
    }
}

class TrieNode {
    TrieNode[] node = new TrieNode[26];
    boolean end;
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```
## Complexity Analysis
```
- Time Complexity: 
  - insert: O(m), where m is the key length.
  - search: O(m)
  - startsWith: O(m)
- Space Complexity: 
  - insert: O(m)
  - search: O(1)
  - startsWith: O(1)
```
