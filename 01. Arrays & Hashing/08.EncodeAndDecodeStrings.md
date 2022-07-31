# 659 · Encode and Decode Strings

Description
Design an algorithm to encode a list of strings to a string. The encoded string is then sent over the network and is decoded back to the original list of strings.

Please implement encode and decode


Example1
```
Input: ["lint","code","love","you"]
Output: ["lint","code","love","you"]
Explanation:
One possible encode method is: "lint:;code:;love:;you"
```
Example2
```
Input: ["we", "say", ":", "yes"]
Output: ["we", "say", ":", "yes"]
Explanation:
One possible encode method is: "we:;say:;:::;yes"
```

```java
public class Solution {
    /*
     * @param strs: a list of strings
     * @return: encodes a list of strings to a single string.
     */
    public String encode(List<String> strs) {
        
        StringBuilder sb = new StringBuilder();
        char seperator = '`';
        for(String str : strs) {
            sb.append(str.length());
            sb.append(seperator);
            sb.append(str);
        }
        return sb.toString();
    }

    /*
     * @param str: A string
     * @return: dcodes a single string to a list of strings
     */
    public List<String> decode(String str) {
        
        List<String> strs = new ArrayList<>();
        int i = 0;
        while(i < str.length()) {
            int j = i;
            while(str.charAt(j) != '`')
                j++;
            int len = Integer.parseInt(str.substring(i, j));
            strs.add(str.substring(j+1, j+1+len));
            i = j + 1 + len;
        }
        return strs; 
    }
}
```
