# [76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)
Hard


Given two strings s and t of lengths m and n respectively, return the minimum window substring of s such that every character in t (including duplicates) is included in the window. If there is no such substring, return the empty string "".

The testcases will be generated such that the answer is unique.

A substring is a contiguous sequence of characters within the string.

 

Example 1:
```
Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
Explanation: The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.
```
Example 2:
```
Input: s = "a", t = "a"
Output: "a"
Explanation: The entire string s is the minimum window.
```
Example 3:
```
Input: s = "a", t = "aa"
Output: ""
Explanation: Both 'a's from t must be included in the window.
Since the largest window of s only has one 'a', return empty string.
``` 

Constraints:
- m == s.length
- n == t.length
- 1 <= m, n <= 105
- s and t consist of uppercase and lowercase English letters.

## Approach
```
- Try to increase the window untill we have all the characters of the pattern
- Once we get the pattern, we update the result if length is less than earlier
- Shrink the window while the window have all the required characters & update the result
```

## Solution
### Approach 1
```java
class Solution {
    public String minWindow(String s, String t) {
        int winS = 0, winE = 0;
        String ans = "";
        Map<Character, Integer> tMp = new HashMap<>();
        Map<Character, Integer> wMp = new HashMap<>();
        for(char c : t.toCharArray()) {
            tMp.put(c, tMp.getOrDefault(c, 0)+1);
        }
        while(winS < s.length() && winE < s.length()) {
            char c = s.charAt(winE);
            wMp.put(c, wMp.getOrDefault(c, 0)+1);
            while(winS <= winE && satisfy(wMp, tMp)) {
                if(ans == "")
                    ans = s.substring(winS, winE+1);
                ans = (winE-winS+1) < ans.length()?s.substring(winS, winE+1):ans;
                wMp.put(s.charAt(winS), wMp.get(s.charAt(winS))-1);
                if(wMp.get(s.charAt(winS)) == 0)
                    wMp.remove(s.charAt(winS));
                winS++;
            }
            winE++;
        }
        return ans;
    }

    private boolean satisfy(Map<Character, Integer> wMp, Map<Character, Integer> tMp) {
        for(char c : tMp.keySet()) {
            if(!wMp.containsKey(c) || wMp.get(c) < tMp.get(c))
                return false;
        }
        return true;
    }
}
```
### Approach 2 (Optimized)
```java
class Solution {
    public String minWindow(String str, String pattern) {
        int windowStart = 0, minLen = Integer.MAX_VALUE, matched = 0;
        Map<Character, Integer> charFreqMap = new HashMap<>();
        String res = "";
        for (char ch : pattern.toCharArray())
            charFreqMap.put(ch, charFreqMap.getOrDefault(ch, 0) + 1);

        for (int windowEnd = 0; windowEnd < str.length(); windowEnd++) {
            char right = str.charAt(windowEnd);

            if (charFreqMap.containsKey(right)) {
                charFreqMap.put(right, charFreqMap.get(right) - 1);
                if (charFreqMap.get(right) == 0)
                    matched++;
            }

            while (matched == charFreqMap.size()) {
                if (minLen > windowEnd - windowStart + 1) {
                    minLen = windowEnd - windowStart + 1;
                    res = str.substring(windowStart, windowEnd + 1);
                }

                char left = str.charAt(windowStart);
                if (charFreqMap.containsKey(left)) {
                    if (charFreqMap.get(left) == 0)
                        matched--;
                    charFreqMap.put(left, charFreqMap.get(left) + 1);
                }
                windowStart++;
            }
        }
        return res;
    }
}
```
## Complexity Analysis
```
Approach 1:
- Time Complexity: O(N*K), N: length of str, K: length of pattern
- Space Complexity: O(K), K: length of pattern
Approach 2:
- Time Complexity: O(N), N: length of str
- Space Complexity: O(K), K: length of pattern
```
