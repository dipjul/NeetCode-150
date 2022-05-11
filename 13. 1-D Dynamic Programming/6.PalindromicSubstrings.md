# [647. Palindromic Substrings](https://leetcode.com/problems/palindromic-substrings/)
Medium

Given a string s, return the number of palindromic substrings in it.

A string is a palindrome when it reads the same backward as forward.

A substring is a contiguous sequence of characters within the string.

 

Example 1:
```
Input: s = "abc"
Output: 3
Explanation: Three palindromic strings: "a", "b", "c".
```
Example 2:
```
Input: s = "aaa"
Output: 6
Explanation: Six palindromic strings: "a", "a", "a", "aa", "aa", "aaa".
 ```

Constraints:

- 1 <= s.length <= 1000
- s consists of lowercase English letters.

## Approach
Reference: [5.LongestPalindromicSubstring](https://github.com/dipjul/NeetCode-150/blob/7961198c07e09a081fec9fbcc445e315bab042a7/13.%201-D%20Dynamic%20Programming/5.LongestPalindromicSubstring.md)
```
Approach 1:
  - expand around every element as a center
  - ood length (i,i)
  - even length (i,i+1)
  - increment for each match
  
Approach 2:
  - Manacher Algorithm
  - every element in p[i]
    - (p[i]+1)/2
```
## Solution
```java
class Solution {
    public int countSubStrings(String s) {
        if (s.length() < 2) {
            return s.length();
        }
        int result = 0;
        for (int i = 0; i < s.length(); i++) {
            // Odd Length
            int left = i, right = i;
            while (left >=0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
                result++;
                left -=1;
                right +=1;
            }
            // Even Length
            left = i;
            right = i + 1;
            while (left >=0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
                result++;
                left -=1;
                right +=1;
            }
        }
        return result;
    } 
}
```
```java
class Solution {
    public int countSubstrings(String s) {
        StringBuilder sb = new StringBuilder();
        sb.append("$");
        for(int i = 0; i < s.length(); i++) {
            sb.append("#");
            sb.append(s.charAt(i));
        }
        sb.append("#");
        sb.append("@");
        int[] p = manacher_odd(sb.toString());
        int ans = 0;
        for(int i = 0; i < p.length; i++)
            ans += (p[i]+1)/2;
        return ans;
    }
    
    private int[] manacher_odd(String s) {
        int[] p = new int[s.length()];
        int center = 0, rightBoundary = 0;
        
        for(int i = 1; i < s.length()-1; i++) {
            
            int mirror = 2*center-i;
            if(i < rightBoundary)
                p[i] = Math.min(p[mirror], rightBoundary-i);
            
            while(s.charAt(i-(p[i]+1)) == s.charAt(i+(p[i]+1)))
                p[i]++;
            
            if(i + p[i] > rightBoundary) {
                center = i;
                rightBoundary = i + p[i];
            }
        }
        
        return p;
    }
}
```
## Complexity Analysis
```
- Time Complexity: 
  - Approach 1: O(N*N)
  - Approach 2: O(N)
- Space Complexity:
  - Approach 1: O(1)
  - Approach 2: O(N)
```
