# 5. Longest Palindromic Substring
Medium


Given a string s, return the longest palindromic substring in s.

 
Example 1:
```
Input: s = "babad"
Output: "bab"
Explanation: "aba" is also a valid answer.
```
Example 2:
```
Input: s = "cbbd"
Output: "bb"
``` 

Constraints:

- 1 <= s.length <= 1000
- s consist of only digits and English letters.

## Approach
```
Approach 1:
  - for each index, try to find odd length & even length palindromes
  - odd: start the inner loop from the same index
  - even: start the inner loop one pointer on i and other at i+1
  - expand towards the left and right of i while the chars are same
  - keep checking the len, and store the start and end
  - substring(start,end+1), end+1 because the substring method takes end index one more than the original end index
  
Approach 2:
- Manacher Algorithm
```
![image](https://user-images.githubusercontent.com/20329508/167583252-2ec3eaf2-24a3-4d26-aa4f-9e315cc8b635.png)

## Solution
```java
class Solution {
    public String longestPalindrome(String s) {
        int resLen = 0, start = 0, end = 0;
        
        if(s == null || s.length() == 0)
            return "";
                
        for(int i = 0; i < s.length(); i++) {
            
            // odd length palindromes
            int left = i, right = i;
            while(left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
                if(right-left+1 > resLen) {
                    start = left;
                    end = right;
                    resLen = right-left+1;
                }
                left--;
                right++;
            }
            
            // even length palindromes
            left = i;
            right = i+1;
            while(left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
                if(right-left+1 > resLen) {
                    start = left;
                    end = right;
                    resLen = right-left+1;
                }
                left--;
                right++;
            }

        }
        
        return s.substring(start, end+1);
    }  
}
```
### Manacher Algorithm
```java
class Solution {
    public String longestPalindrome(String s) {
        StringBuilder sb = new StringBuilder();
        // appending chars before, inbetween and end to make the string
        // such that we can use the manacher odd algorithm
        sb.append("$");
        for(int i = 0; i < s.length(); i++) {
            sb.append("#");
            sb.append(s.charAt(i));
        }
        sb.append("#");
        sb.append("&");
        
        int[] p = manacher_odd(sb.toString());
        int center = 0, resLen = 0;
        for(int i = 0; i < p.length; i++) {
            if(p[i] > resLen) {
                center = i;
                resLen = p[i];
            }
        }
        
        return s.substring((center-resLen)/2, (center+resLen)/2);
    }
    
    private int[] manacher_odd(String s) {
        int[] p = new int[s.length()]; // max palindromes length centered at the index
        int center = 0; // center is to keep the new center
        int rightBoundary = 0; // rightBoundary to keep the boundary
        
        for(int i = 1; i < s.length()-1; i++) {
            // find the mirror [..mirror...center...i..]
            int mirror = 2*center-i;
            
            // if i is inside the boundary then only we can assign the value
            if(i < rightBoundary)
                p[i] = Math.min(p[mirror], rightBoundary-i);
            
            // while the chars are matching keep incrementing p[i] 
            // which interns result into match the next chars to the left and right
            while(s.charAt(i-(p[i]+1)) == s.charAt(i+(p[i]+1)))
                p[i]++;
            
            // if the palindrome with centered i, exceeds the right boundary
            // then we need to update the right boundary and the new center
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
