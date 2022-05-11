# [91. Decode Ways](https://leetcode.com/problems/decode-ways/)
Medium


A message containing letters from A-Z can be encoded into numbers using the following mapping:

'A' -> "1"

'B' -> "2"

...

'Z' -> "26"

To decode an encoded message, all the digits must be grouped then mapped back into letters using the reverse of the mapping above (there may be multiple ways). For example, "11106" can be mapped into:

`"AAJF" with the grouping (1 1 10 6)`

`"KJF" with the grouping (11 10 6)`

Note that the grouping (1 11 06) is invalid because "06" cannot be mapped into 'F' since "6" is different from "06".

Given a string s containing only digits, return the number of ways to decode it.

The test cases are generated so that the answer fits in a 32-bit integer.

 

Example 1:
```
Input: s = "12"
Output: 2
Explanation: "12" could be decoded as "AB" (1 2) or "L" (12).
```
Example 2:
```
Input: s = "226"
Output: 3
Explanation: "226" could be decoded as "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).
```
Example 3:
```
Input: s = "06"
Output: 0
Explanation: "06" cannot be mapped to "F" because of the leading zero ("6" is different from "06").
 ```

Constraints:

- 1 <= s.length <= 100
- s contains only digits and may contain leading zero(s).

## Approach
```
- Approach
  - take an dp array of size 1 greater than len(s)
  - at the last index we'll keep 1
  - for every char, if char not equal of 0
    - dp[i] += dp[i+1]
    - if s(i,i+2) is < 26
      - dp[i] += dp[i+2]
  - at last we'll have the ans at dp[0]

- Optimize
  - pattern seems like fibonacci
  - we can replace the array with three variables
    - curr will have dp[i]
    - prev will have dp[i+1]
    - prev2 will have dp[i+2]
  
```

## Solution
```java
class Solution {
    
    public int numDecodings(String s) {
        int n = s.length();
        int[] dp = new int[n+1];
        dp[n] = 1;
        
        for(int i = n-1; i >= 0; i--) {
            char ch = s.charAt(i);
            if(ch != '0') {
                dp[i] += dp[i+1];
                if(i < n-1 && Integer.valueOf(s.substring(i,i+2)) <= 26)
                    dp[i] += dp[i+2];
            }
        }
        return dp[0];
    }
      // Optimized
      public int numDecodings(String s) {
        int n = s.length();
        
        int prev = 1, prev2 = 0, curr = 0;
        
        for(int i = n-1; i >= 0; i--) {
            char ch = s.charAt(i);
            curr = 0;
            if(ch != '0') {
                curr += prev;
                if(i < n-1 && ((ch-'0' == 1) || (ch-'0' <= 2 && s.charAt(i+1)-'0' <= 6)))
                    curr += prev2;
            }
            int tmp = prev;
            prev = curr;
            prev2 = tmp;
        }
        return curr;
    }
}
```

## Complexity Analysis
```
- Time Complexity:
  - Approach 1 & Approach 2: O(N)
- Space Complexity:
  - Approach 1: O(N), dp array of n size
  - Approach 2: O(1), 3 variables

```
