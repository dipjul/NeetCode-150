# 567. Permutation in String
Medium


Given two strings s1 and s2, return true if s2 contains a permutation of s1, or false otherwise.

In other words, return true if one of s1's permutations is the substring of s2.

 

Example 1:
```
Input: s1 = "ab", s2 = "eidbaooo"
Output: true
Explanation: s2 contains one permutation of s1 ("ba").
```
Example 2:
```
Input: s1 = "ab", s2 = "eidboaoo"
Output: false
 ```

Constraints:

- 1 <= s1.length, s2.length <= 10<sup>4</sup>
- s1 and s2 consist of lowercase English letters.

## Approach
```
- 2 array of size 26 to keep count of chars present in both the strings[s1 and substring of s2]
- match keeps the number of characters matches in both s1 and substring of s2
- if matches = 26, we have a permutation in that window
- on each window, we check for conditions [ for both the chars(at left and at right) ]:
  - increment s2Map[rightCharInd]++ and decrement s2Map[leftCharInd]--
  - if the char's count are same increment the matches
  - if the char's count differ by 1 
    - right: s1Map[rightCharInd] + 1 == s2Map[rightCharInd], 
    - left: s1Map[leftCharInd] - 1 == s2Map[leftCharInd] decrement the matches
```

## Solution
```java
class Solution {
    public boolean checkInclusion(String s1, String s2) {
        if(s1.length() > s2.length())
            return false;
        char[] s1Map = new char[26];
        char[] s2Map = new char[26];
        
        for(int i = 0; i < s1.length(); i++) {
            s1Map[s1.charAt(i)-'a']++;
            s2Map[s2.charAt(i)-'a']++;
        }
            
        int matches = 0;
        for(int i = 0; i < 26; i++) {
            if(s1Map[i] == s2Map[i])
                matches++;
        }
        int windowStart = 0;
        for(int windowEnd = s1.length(); windowEnd < s2.length(); windowEnd++) {
            if(matches == 26) return true;
            int rightCharInd = s2.charAt(windowEnd)-'a';
            s2Map[rightCharInd]++;
            if(s1Map[rightCharInd] == s2Map[rightCharInd])
                matches++;
            else if(s1Map[rightCharInd] + 1 == s2Map[rightCharInd])
                matches--;
            
            int leftCharInd = s2.charAt(windowStart)-'a';
            s2Map[leftCharInd]--;
            if(s1Map[leftCharInd] == s2Map[leftCharInd])
                matches++;
            else if(s1Map[leftCharInd] - 1 == s2Map[leftCharInd])
                matches--;
            
            windowStart++;
        }
        
        return matches == 26;
    }
}
```
## Complexity Analysis:
```
Time Complexity: O(s2.length())
Space Complexity: O(26) ~ O(1)
```
