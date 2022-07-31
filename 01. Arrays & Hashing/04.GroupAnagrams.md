# 49. Group Anagrams
Medium


Given an array of strings strs, group the anagrams together. You can return the answer in any order.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

 

Example 1:
```
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
```
Example 2:
```
Input: strs = [""]
Output: [[""]]
```
Example 3:
```
Input: strs = ["a"]
Output: [["a"]]
 ```

Constraints:

- 1 <= strs.length <= 104
- 0 <= strs[i].length <= 100
- strs[i] consists of lowercase English letters.

```java
class Solution {
    // 1
    public List<List<String>> groupAnagrams(String[] strs) {
        List<List<String>> res = new ArrayList<>();
        Map<String, List<String>> mp = new HashMap<>();
        for (String str : strs) {
            char[] c = str.toCharArray();
            Arrays.sort(c);
            String r = new String(c);
            if (!mp.containsKey(r))
                mp.put(r, new ArrayList<String>());
            mp.get(r).add(str);
        }
        for (String key : mp.keySet()) {
            res.add(mp.get(key));
        }

        return res;
    }
  
    // 2
    public List<List<String>> groupAnagrams(String[] strs) {
        List<List<String>> res = new ArrayList<>();
        Map<String, List<String>> mp = new HashMap<>();
        for (String str : strs) {
            char[] hash = new char[26];
            for(char ch : str.toCharArray())
                hash[ch-'a']++;
            String r = new String(hash);
            if (!mp.containsKey(r))
                mp.put(r, new ArrayList<String>());
            mp.get(r).add(str);
        }
        for (String key : mp.keySet()) {
            res.add(mp.get(key));
        }

        return res;
    }
    
}
```
