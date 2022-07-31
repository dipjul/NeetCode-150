# [50. Pow(x, n)](https://leetcode.com/problems/powx-n/)
Medium


Implement pow(x, n), which calculates x raised to the power n (i.e., xn).

 

Example 1:
```
Input: x = 2.00000, n = 10
Output: 1024.00000
```
Example 2:
```
Input: x = 2.10000, n = 3
Output: 9.26100
```
Example 3:
```
Input: x = 2.00000, n = -2
Output: 0.25000
Explanation: 2-2 = 1/22 = 1/4 = 0.25
 ```

Constraints:

- -100.0 < x < 100.0
- -2<sup>31</sup> <= n <= 2<sup>31</sup>-1
- -10<sup>4</sup> <= xn <= 10<sup>4</sup>

## Approach
```
- Recursiom:
- we can divide the power by 2 and same value can be reused
- For non-negative:
  - for even: pow(x, n) = pow(x, n/2)*pow(x,n/2)
  - for odd: - for even: pow(x, n) = x*pow(x, n/2)*pow(x,n/2)
- For negative:
  - for even: pow(x, n) = pow(x, n/2)*pow(x,n/2)
  - for odd: - for even: pow(x, n) = 1/x*pow(x, n/2)*pow(x,n/2)
```
## Solution
```java
class Solution {
    public double myPow(double x, int n) {
        if(n < 0)
            return myPowNeg(x, n);
        return myPowPos(x, n);
    }
    
    private double myPowNeg(double x, int n) {
        if(x == 1 || n == 0)
            return 1;
        if(n == -1)
            return 1/x;
        double ans = myPow(x, n/2);
        ans *= ans;
        if(n%2 != 0)
            return ans/x;
        return ans;
    }
    
    private double myPowPos(double x, int n) {
        if(x == 1 || n == 0)
            return 1;
        double ans = myPow(x, n/2);
        ans *= ans;
        if(n%2 != 0)
            return ans*x;
        return ans;
    }
}
```
## Complexity Analysis
```
- Time Complexity: O(logn)
- Space Complexity: O(logn)
```
