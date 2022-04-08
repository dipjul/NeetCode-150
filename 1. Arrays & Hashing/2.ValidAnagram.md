# 242. Valid Anagram
Easy

Given two strings s and t, return true if t is an anagram of s, and false otherwise.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

 

Example 1:
```
Input: s = "anagram", t = "nagaram"
Output: true
```
Example 2:
```
Input: s = "rat", t = "car"
Output: false
 ```

Constraints:

- 1 <= s.length, t.length <= 5 * 104
- s and t consist of lowercase English letters.
 
```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if(s.length() != t.length())
            return false;
        
        int[] chars = new int[26];
        
        for(int i = 0; i < s.length(); i++) {
            chars[s.charAt(i)-'a']++;
            chars[t.charAt(i)-'a']--;
        }
            
        
        for(int n : chars) {
            if(n != 0)
                return false;
        }
        
        return true;
    }
}
```

### Follow up: What if the inputs contain Unicode characters? How would you adapt your solution to such a case?
We can be used a map, or a array of size equal to the characterset size of unicode.
