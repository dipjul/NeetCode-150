# 74. Search a 2D Matrix
Medium


Write an efficient algorithm that searches for a value target in an m x n integer matrix matrix. This matrix has the following properties:

Integers in each row are sorted from left to right.
The first integer of each row is greater than the last integer of the previous row.
 

Example 1:
```
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
Output: true
```
Example 2:
```
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13
Output: false
``` 

Constraints:

- m == matrix.length
- n == matrix[i].length
- 1 <= m, n <= 100
- -10<sup>4</sup> <= matrix[i][j], target <= 10<sup>4</sup>

## Approach
```
1st:
- keep two pointer one for row, other for column
- initialize tem to point to the last element of the 1st row
- if the element is equal to target then return true
- else if element is < target then move the row pointer downward
- else shift the column pointer to left

2nd: 
[It would work only when the element at 1st index of next row should be greater then last element of the previous row]
- left pointer at 0, right at n*m-1 (at last element of the matrix)
- do the binarysearch
- target element can be find using 
  - rowIndex = mid / number of elements in each row
  - colIndex = mid % number of elements in each row
```

## Solution
```java
class Solution {
    // worst case go through O(n+m) elements
    public boolean searchMatrix(int[][] matrix, int target) {
        int m = matrix.length, n = matrix[0].length;
        int row = 0, col = n-1;
        while(row >= 0 && row < m && col >= 0 && col < n) {
            int val = matrix[row][col];
            if(val == target)
                return true;
            else if(val < target)
                row++;
            else
                col--;
        }
        return false;
    }
    
    // worst case it would go through O(log(n*m)) elements
    public boolean searchMatrix1(int[][] matrix, int target) {
        int m = matrix.length, n = matrix[0].length;
        int left = 0, right = m*n-1;
        while(left <= right) {
            int mid = left + (right-left)/2;
            int val = matrix[mid/n][mid%n];
            if(val == target)
                return true;
            else if(val < target)
                left = mid+1;
            else
                right = mid-1;
        }
        return false;
    }
}
```

## Complexity Analysis
```
- Time Complexity:
  - 1st approach: O(n+m)
  - 2nd approach: O(log(n*m))
- Space Coplexity: O(1) for both approaches
```
