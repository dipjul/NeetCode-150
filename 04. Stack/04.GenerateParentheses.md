# 22. Generate Parentheses
Medium


Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

 > Feels like mismatch for the pattern satck 

Example 1:
```
Input: n = 3
Output: ["((()))","(()())","(())()","()(())","()()()"]
```
Example 2:
```
Input: n = 1
Output: ["()"]
 ```

Constraints:

- 1 <= n <= 8

## Approach
```
- Backtracking
- add '(' always and add ')' only if count('(') > count(')')
- add the string into the result when count('(') > count(')') && count('(') == n
- base case: count('(') > n || count(')') > n
```

## Solution
```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> ans = new ArrayList<>(); 
        generate(0, n, 0, 0, ans, "");
        return ans;
    }
    
    private void generate(int index, int n, int lCount, int rCount, List<String> ans, String op) {
        if(lCount > n || rCount > n)
            return;
        if(lCount == rCount && lCount == n) {
            ans.add(op);
        }
        if(lCount > rCount) {
            String op1 = op + ")";
            generate(index+1, n, lCount, rCount+1, ans, op1);
        }
        String op2 = op + "(";
        generate(index+1, n, lCount+1, rCount, ans, op2);
    }
}
```
