# 54. Spiral Matrix
Medium


Given an m x n matrix, return all elements of the matrix in spiral order.

 

Example 1:
```
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,3,6,9,8,7,4,5]
```
Example 2:
```
Input: matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
Output: [1,2,3,4,8,12,11,10,9,5,6,7]
 ```

Constraints:

- m == matrix.length
- n == matrix[i].length
- 1 <= m, n <= 10
- -100 <= matrix[i][j] <= 100

## Approach
```

```

## Solution
```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> res = new ArrayList<>();
        int m = matrix.length - 1;
        int n = matrix[0].length - 1;
        int sr = 0, sc = 0;
        int i = sr, j = sc;
        while (sc <= n || sr <= m) {

            // 1st row
            while (j <= n) {
                res.add(matrix[i][j]);
                j++;
            }
            sr++;
            j = n;
            i = sr;

            // condition
            if (i > m || j > n) {
                break;
            }
            // last colunm
            while (i <= m) {
                res.add(matrix[i][j]);
                i++;
            }
            n--;
            i = m;
            j = n;

            if (i > m || j > n) {
                break;
            }

            // last row
            while (j >= sc) {
                res.add(matrix[i][j]);
                j--;
            }
            m--;
            j = sc;
            i = m;

            if (i > m || j > n) {
                break;
            }
            // 1st column
            while (i >= sr) {
                res.add(matrix[i][j]);
                i--;
            }
            sc++;
            i = sr;
            j = sc;

            if (i > m || j > n) {
                break;
            }
        }
        return res;
    }
}
```

## Complexity Analysis
```
- Time Complexity: O(n), n : number of elements in the matrix
- Space Complexity: O(1)
```
