# 424. Longest Repeating Character Replacement
Medium


You are given a string s and an integer k. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most k times.

Return the length of the longest substring containing the same letter you can get after performing the above operations.

 

Example 1:
```
Input: s = "ABAB", k = 2
Output: 4
Explanation: Replace the two 'A's with two 'B's or vice versa.
```
Example 2:
```
Input: s = "AABABBA", k = 1
Output: 4
Explanation: Replace the one 'A' in the middle with 'B' and form "AABBBBA".
The substring "BBBB" has the longest repeating letters, which is 4.
``` 

Constraints:

- 1 <= s.length <= 10<sup>5</sup>
- s consists of only uppercase English letters.
- 0 <= k <= s.length

## Notes
```
- use a map to store the frequency
- maxRepeatingCharCount = max(maxRepeatingCharCount, mp.get(char))
- slide the left pointer until the equation satifies: windowEnd - windowStart + 1 - maxRepeatingCharCount > k
- maxLen = max(maxLen, windowEnd - windowStart + 1)
```

## Solution:
```java
class Solution {
    public int characterReplacement(String s, int k) {
        int windowStart = 0, maxLength = 0, mostRepeatingCharCount = 0;
        
        HashMap<Character, Integer> charFreqMap = new HashMap();
        
        for(int windowEnd = 0; windowEnd < s.length(); windowEnd++) {
            char right = s.charAt(windowEnd);
            charFreqMap.put(right, charFreqMap.getOrDefault(right, 0)+1);
            mostRepeatingCharCount = Math.max(mostRepeatingCharCount, charFreqMap.get(right));
            
            while(windowEnd-windowStart+1 - mostRepeatingCharCount > k) {
                char left = s.charAt(windowStart);
                charFreqMap.put(left, charFreqMap.get(left)-1);
                if(charFreqMap.get(left) == 0)
                    charFreqMap.remove(left);
                windowStart++;
            }
            maxLength = Math.max(maxLength, windowEnd-windowStart+1);
        }
        
        return maxLength;
    }
}
```
