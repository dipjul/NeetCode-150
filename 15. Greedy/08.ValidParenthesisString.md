# [678. Valid Parenthesis String](https://leetcode.com/problems/valid-parenthesis-string/)
Medium


Given a string s containing only three types of characters: '(', ')' and '*', return true if s is valid.

The following rules define a valid string:

Any left parenthesis '(' must have a corresponding right parenthesis ')'.
Any right parenthesis ')' must have a corresponding left parenthesis '('.
Left parenthesis '(' must go before the corresponding right parenthesis ')'.
'*' could be treated as a single right parenthesis ')' or a single left parenthesis '(' or an empty string "".
 

Example 1:
```
Input: s = "()"
Output: true
```
Example 2:
```
Input: s = "(*)"
Output: true
```
Example 3:
```
Input: s = "(*))"
Output: true
 ```

Constraints:

1 <= s.length <= 100
s[i] is '(', ')' or '*'.

## Approach
```
Approach 1:
  - backtrack
  - count+1 if '('
  - count-1 if ')'
  - For '*':
    - 3 calls: count+1, count-1, count+0
  - dp (index, count) = true/false
  
Approach 2: greedy
```

## Solution
```java
class Solution {
    Boolean[][] dp;

    public boolean checkValidString(String s) {
        dp = new Boolean[s.length()][s.length()];
        return backtrack(s, 0, 0);
    }

    private boolean backtrack(String s, int index, int count) {
        if (count < 0 || (index >= s.length() && count > 0))
            return false;
        if (index >= s.length() && count == 0)
            return true;
        if (dp[index][count] != null)
            return dp[index][count];
        if (s.charAt(index) == '*') {
            dp[index][count] = (backtrack(s, index + 1, count + 1) ||
                    backtrack(s, index + 1, count - 1) ||
                    backtrack(s, index + 1, count));
        } else if (s.charAt(index) == '(') {
            dp[index][count] = backtrack(s, index + 1, count + 1);
        } else {
            dp[index][count] = backtrack(s, index + 1, count - 1);
        }
        return dp[index][count];
    }
}
```
```java
public class ValidString {
    public static boolean isValid(String str) {
        int leftMin = 0, leftMax = 0;
        for (char ch: str.toCharArray()) {
            if (ch == '(') {
                leftMin++;
                leftMax++;
            }
            else if (ch == ')') {
                leftMin--;
                leftMax--;
            }
            else {
                leftMin--;
                leftMax++;
            }
            if (leftMax < 0) { // Means we encounter ) as a starting character or # of occurrences of ) is > (
                return false;
            }
            if (leftMin < 0) {
                leftMin = 0;
            }
        }
        return leftMin == 0;
    }
}
```

## Complexity Analysis
```
- Time Complexity: 
  - Approach 1: O(n^3)
  - Approach 2: O(n)
- Space Complexity: 
  - Approach 1: O(n)
  - Approach 2: O(1)
```
