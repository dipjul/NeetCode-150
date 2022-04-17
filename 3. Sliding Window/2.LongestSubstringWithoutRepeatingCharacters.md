# 3. Longest Substring Without Repeating Characters
Medium


Given a string s, find the length of the longest substring without repeating characters.

 

Example 1:
```
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```
Example 2:
```
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```
Example 3:
```
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
 ```

Constraints:

- 0 <= s.length <= 5 * 104
- s consists of English letters, digits, symbols and spaces.

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        Map<Character, Integer> mp = new HashMap<>();
        int maxLen = 0, winStart = 0;
        
        for(int winEnd = 0; winEnd < s.length(); winEnd++) {
            char ch = s.charAt(winEnd);
            if(mp.containsKey(ch)) {
                winStart = Math.max(winStart, mp.get(ch)+1);
            }
            mp.put(ch, winEnd);
            maxLen = Math.max(winEnd - winStart + 1, maxLen);
        }
        return maxLen;        
    }
}
```
