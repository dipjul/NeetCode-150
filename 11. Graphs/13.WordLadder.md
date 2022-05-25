# [127. Word Ladder](https://leetcode.com/problems/word-ladder/)
Hard


A transformation sequence from word beginWord to word endWord using a dictionary wordList is a sequence of words `beginWord -> s1 -> s2 -> ... -> sk` such that:

- Every adjacent pair of words differs by a single letter.
- Every si for 1 <= i <= k is in wordList. Note that beginWord does not need to be in wordList.
- sk == endWord

Given two words, beginWord and endWord, and a dictionary wordList, return the number of words in the shortest transformation sequence from beginWord to endWord, or 0 if no such sequence exists.

 

Example 1:
```
Input: beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"]
Output: 5
Explanation: One shortest transformation sequence is "hit" -> "hot" -> "dot" -> "dog" -> cog", which is 5 words long.
```
Example 2:
```
Input: beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log"]
Output: 0
Explanation: The endWord "cog" is not in wordList, therefore there is no valid transformation sequence.
``` 

Constraints:

- 1 <= beginWord.length <= 10
- endWord.length == beginWord.length
- 1 <= wordList.length <= 5000
- wordList[i].length == beginWord.length
- beginWord, endWord, and wordList[i] consist of lowercase English letters.
- beginWord != endWord
- All the words in wordList are unique.

## Approach
```
- Add the begin word to the wordList
- Create a graph such that neighbours of each node is differ by one character
  - eg. fog would be neighbour of cog
- if endWord not present in the graph return 0
- How to find if two words are neighbour?
  - Loop through the two words, whenever it differs increment the count
    - if count == 1 return true else false
- Start bfs search from the beginWord untill we reach the endWord
  - Keep count of distance from beginWord, return distance 
```

## Solution
```java
class Solution {

    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        Map<String, List<String>> graph = new HashMap<>();
        wordList.add(0, beginWord);
        for (int i = 0; i < wordList.size(); i++) {
            for (int j = i + 1; j < wordList.size(); j++) {
                String s1 = wordList.get(i);
                String s2 = wordList.get(j);
                if (differByOne(s1, s2)) {
                    List<String> arr1 = graph.getOrDefault(s1, new ArrayList<>());
                    arr1.add(s2);
                    List<String> arr2 = graph.getOrDefault(s2, new ArrayList<>());
                    arr2.add(s1);
                    graph.put(s1, arr1);
                    graph.put(s2, arr2);
                }
            }
        }
        
        if (!graph.containsKey(endWord)) return 0;

        Queue<String> q = new LinkedList<>();

        q.offer(beginWord);

        if (q.size() == 0) return 0;
        Set<String> visited = new HashSet<>();
        int pathSize = 0;
        while (!q.isEmpty()) {
            int size = q.size();
            pathSize++;
            for (int i = 0; i < size; i++) {
                String s1 = q.poll();
                visited.add(s1);
                if (s1.equals(endWord)) return pathSize;
                for (String s : graph.get(s1)) {
                    if (!visited.contains(s)) q.offer(s);
                }
            }
        }

        return 0;
    }

    private boolean differByOne(String word1, String word2) {
        if (word1.length() != word2.length()) return false;
        int n = word1.length();
        int count = 0;
        for (int i = 0; i < n; i++) {
            if (word1.charAt(i) != word2.charAt(i)) {
                count++;
                if (count > 1) return false;
            }
        }
        return count == 1;
    }
}

```

## Complexity Analysis
```
- Time Complexity: O(n*n)
- Space Complexity: O(n+m)
```
