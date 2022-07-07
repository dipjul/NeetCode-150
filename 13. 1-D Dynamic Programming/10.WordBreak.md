# [139. Word Break](https://leetcode.com/problems/word-break/)
Medium


Given a string s and a dictionary of strings wordDict, return true if s can be segmented into a space-separated sequence of one or more dictionary words.

Note that the same word in the dictionary may be reused multiple times in the segmentation.

 

Example 1:
```
Input: s = "leetcode", wordDict = ["leet","code"]
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".
```
Example 2:
```
Input: s = "applepenapple", wordDict = ["apple","pen"]
Output: true
Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".
Note that you are allowed to reuse a dictionary word.
```
Example 3:
```
Input: s = "catsandog", wordDict = ["cats","dog","sand","and","cat"]
Output: false
 ```

Constraints:

- 1 <= s.length <= 300
- 1 <= wordDict.length <= 1000
- 1 <= wordDict[i].length <= 20
- s and wordDict[i] consist of only lowercase English letters.
- All the strings of wordDict are unique.

## Approach
### Decision tree of Backtracking
![image](https://user-images.githubusercontent.com/20329508/177688399-84392e46-3da0-4d19-9228-fb952ef77022.png)

### Cache
![image](https://user-images.githubusercontent.com/20329508/177688529-5ba87230-2455-4680-a805-650652005975.png)

### Bottom up
![image](https://user-images.githubusercontent.com/20329508/177689013-929cba9b-8767-46e4-a5b7-c2186727b258.png)

```
- start from last index
- if index + len of word from dict is less than eqaul to n and substring of s from index to index + len(word) is equal to word
 - dp[index] = dp[index + len(word)]
 - if dp[index] is true move to next index
- dp[0] would have the result
```

## Solution
```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        int n = s.length();
        boolean dp[] = new boolean[n+1];
        dp[n] = true;
        
        for(int i = n-1; i >= 0; i--) {
            for(String w : wordDict) {
                if(i + w.length() <= n && w.equals(s.substring(i, i+w.length())))
                    dp[i] = dp[i + w.length()];
                
                if(dp[i])
                    break;
            }
        }
        return dp[0];
    }
}
```

## Complexity Analysis
```
- Time Complexity: O(N*len(wordInDict))
- Space Complexity: O(N)
```
