# [43. Multiply Strings](https://leetcode.com/problems/multiply-strings/)
Medium


Given two non-negative integers num1 and num2 represented as strings, return the product of num1 and num2, also represented as a string.

Note: You must not use any built-in BigInteger library or convert the inputs to integer directly.

 

Example 1:
```
Input: num1 = "2", num2 = "3"
Output: "6"
```
Example 2:
```
Input: num1 = "123", num2 = "456"
Output: "56088"
 ```

Constraints:

- 1 <= num1.length, num2.length <= 200
- num1 and num2 consist of digits only.
- Both num1 and num2 do not contain any leading zero, except the number 0 itself.

## Approach
```
- Reverse the number strings
- StringBuilder(mutable string) of 400 size, as num1 & num2 of 200 length at max
- calculate the multiplication and store overwrite it at the i+j position
- after each inner loop, we insert the carry at i+j position, j would be 1 position more the the original length of the second number
- reverse the string
- remove all the leading 0s
- return 0 if result string size is zero or else return thr result string
```

## Solution
```java
class Solution {
    public String multiply(String num1, String num2) {
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < 400; i++)
            sb.append(0);
        num1 = reverse(num1);
        num2 = reverse(num2);
        if(num1.length() > num2.length()) {
            String tmp = num1;
            num1  = num2;
            num2 = tmp;
        }
        int carry = 0;
        int i = 0, j = 0;
        for (i = 0; i < num2.length(); i++) {
            carry = 0;
            for (j = 0; j < num1.length(); j++) {
                int a =  num2.charAt(i)-'0';
                int b = num1.charAt(j)-'0';
                int n = a * b + carry;
                int prev = sb.charAt(i+j)-'0';
                int sum = (prev + n) % 10;
                carry = (n+prev) / 10;
                sum +='0';
                sb.setCharAt(i + j, (char) sum);
            }
            sb.setCharAt(i+j, (char) (carry+'0'));
        }

        sb.setCharAt(i+j-1, (char) (carry+'0'));
        sb.reverse();
        int ind = 0;
        while(sb.length() > 0 && sb.charAt(ind) == '0')
            sb.deleteCharAt(ind);
        return sb.length() == 0?"0":sb.toString();
    }

    private String reverse(String s) {
        StringBuilder sb = new StringBuilder(s);
        sb.reverse();
        return sb.toString();
    }
}

```

## Complexity Analysis
```
- Time Compexity: O(n*m)
- Space Complexity: O(400)
```
