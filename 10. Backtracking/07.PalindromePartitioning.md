# [131. Palindrome Partitioning](https://leetcode.com/problems/palindrome-partitioning/)
Medium


Given a string s, partition s such that every substring of the partition is a palindrome. Return all possible palindrome partitioning of s.

A palindrome string is a string that reads the same backward as forward.

 

Example 1:
```
Input: s = "aab"
Output: [["a","a","b"],["aa","b"]]
```
Example 2:
```
Input: s = "a"
Output: [["a"]]
 ```

Constraints:

- 1 <= s.length <= 16
- s contains only lowercase English letters.

## Approach
```
- backtracking
- go through all possible combination of substring
- if the substring is palindrome add it to the tmp result and backtrack
- if substring becomes empty then add tmp result to the result

```

## Solution
```java
class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> result = new ArrayList();
        helper(s, new ArrayList<String>(), result);
        return result;
    }
    
    public void helper(String s, List<String> step, List<List<String>> result) {
        if(s == null || s.length() == 0) {
            result.add(new ArrayList<>(step));
            return;
        }
        
        for(int i = 1; i <= s.length(); i++) {
            String temp = s.substring(0, i);
            if(isPalindrome(temp)){
                step.add(temp);
                helper(s.substring(i, s.length()), step, result);
                step.remove(step.size()-1);
            }
        }
        return;
    }
    
    private boolean isPalindrome(String s) {
        int start = 0, end = s.length()-1;
        while(start <= end) {
            if(s.charAt(start++) != s.charAt(end--))
                return false;
        }
        return true;
    }
}

```

## Complexity Analysis
```
- Time Complexity: O(N*2^N)
- Space Complexity: O(N)
```
