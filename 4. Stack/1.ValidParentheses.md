# 20. Valid Parentheses
Easy


Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

- Open brackets must be closed by the same type of brackets.
- Open brackets must be closed in the correct order.
 

Example 1:
```
Input: s = "()"
Output: true
```
Example 2:
```
Input: s = "()[]{}"
Output: true
```
Example 3:
```
Input: s = "(]"
Output: false
 ```

Constraints:

- 1 <= s.length <= 104
- s consists of parentheses only '()[]{}'.

```java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> st = new Stack<>();
        
        for(int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if(c == '(' || c == '{' || c == '[')
                st.push(c);
            else if(c == ')' && !st.empty()) {
                char ch = st.pop();
                if(ch != '(')
                    return false;
            } else if(c == '}' && !st.empty()) {
                char ch = st.pop();
                if(ch != '{')
                    return false;
            } else if(c == ']' && !st.empty()) {
                char ch = st.pop();
                if(ch != '[')
                    return false;
            } else
                return false;
        }
        
        return st.empty();
    }
}
```
