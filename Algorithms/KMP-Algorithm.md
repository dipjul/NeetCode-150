# KMP String matching algorithm

## 28. Implement strStr()
Easy

Implement strStr().

Given two strings needle and haystack, return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

Clarification:

What should we return when needle is an empty string? This is a great question to ask during an interview.

For the purpose of this problem, we will return 0 when needle is an empty string. This is consistent to C's strstr() and Java's indexOf().

 

Example 1:

Input: haystack = "hello", needle = "ll"
Output: 2
Example 2:

Input: haystack = "aaaaa", needle = "bba"
Output: -1
 

Constraints:

- 1 <= haystack.length, needle.length <= 10<sup>4</sup>
- haystack and needle consist of only lowercase English characters.

## Approach
```
- build pattern:
  - we build the pattern for the substring
  - it would be use in matching the pattern
  - how:
    - initialize two pointers, starting from 0(j) and 1(i)
    - while i < len(substring)
      - if s[i] == s[j] then set pattern[i] = j and increment both pointers, (which means we found a suffix that matches a prefix)
      - else if j > 0 then set j to pattern[j-1]+1, (j-1 holds the last index where it had a successful match)
      - else increment i
- matching pattern
  - similar to build pattern
  - how:
    - initialize two pointers, starting from 0(j) points to sunstring and 0(i) points to string
    - while i + len(substring) - j <= len(string)
      - if s[i] == s[j] 
        - if j = len(substring)-1
          - we found the match
        - increment both pointers,
      - else if j > 0 then set j to pattern[j-1]+1, (j-1 holds the last index where it had a successful match)
      - else increment i
```
## Solution
```java
class Solution {
    public int strStr(String haystack, String needle) {
        int[] pattern = new int[needle.length()];
        Arrays.fill(pattern, -1);
        buildPattern(needle, pattern);
        return matchIndex(haystack, needle, pattern);
    }
    
    private void buildPattern(String str, int[] pattern) {
        int j = 0;
        int i = 1;
        while(i < str.length()) {
            if(str.charAt(i) == str.charAt(j)) {
                pattern[i] = j;
                i++;
                j++;
            } else if(j > 0) {
                j = pattern[j-1] + 1;
            } else {
                i++;
            }
        }
    }
    
    private int matchIndex(String str, String substr, int[] pattern) {
        int j = 0, i = 0;
        
        while(i + substr.length() - j <= str.length()) {
            if(str.charAt(i) == substr.charAt(j)) {
                if(j == substr.length()-1)
                    return i-j;
                i++;
                j++;
            } else if(j > 0) {
                j = pattern[j-1] + 1;
            } else {
                i++;
            }
        }
        return -1;
    }
}
```
## Complexity Analysis
```
- Time Complexity: O(n+m), n - length of string, m - length of substring
- Space Complexity: O(m), to build the pattern array
```
