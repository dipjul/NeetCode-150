# [17. Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)
Medium


Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. Return the answer in any order.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.



 

Example 1:
```
Input: digits = "23"
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]
```
Example 2:
```
Input: digits = ""
Output: []
```
Example 3:
```
Input: digits = "2"
Output: ["a","b","c"]
 ```

Constraints:

- 0 <= digits.length <= 4
- digits[i] is a digit in the range ['2', '9'].

## Approach
```
Backtrack:
char chs[] = mp.get(str.charAt(i));
for(int j = 0; j < chs.length; j++) {
    recursive(str, i+1, s+chs[j], res); - stmt
}
stmt is equivalent to:
String s = s+chs[j];
recursive(str, i+1, s, res);
s = s.substring(0,s.length()-1);
```

## Solution
```java
class Solution {
    Map<Character, char[]> mp;
    public List<String> letterCombinations(String digits) {
        if(digits.equals(""))
            return new ArrayList<>();
        mp = new HashMap<>();
        mp.put('2', new char[]{'a', 'b', 'c'});
        mp.put('3', new char[]{'d', 'e', 'f'});
        mp.put('4', new char[]{'g', 'h', 'i'});
        mp.put('5', new char[]{'j', 'k', 'l'});
        mp.put('6', new char[]{'m', 'n', 'o'});
        mp.put('7', new char[]{'p', 'q', 'r', 's'});
        mp.put('8', new char[]{'t', 'u', 'v'});
        mp.put('9', new char[]{'w', 'x', 'y', 'z'});
        List<String> res = new ArrayList<>();
        recursive(digits, 0, "", res);
        return res;
    }
    
    private void recursive(String str, int i, String s, List<String> res) {
        if(i > str.length())
            return;
        if(i == str.length()) {
            res.add(s);
            return;
        }
        char chs[] = mp.get(str.charAt(i));
        for(int j = 0; j < chs.length; j++) {
            recursive(str, i+1, s+chs[j], res);
        }
        
    }
}
```

## Complexity Analysis
```
- Time Complexity:
- Space Complexity:
```
