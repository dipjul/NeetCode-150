# Fenwick Tree
## Introduction

## Approach

## Implementation
```java
public class FenwickTree2D {
    int[][] ft;

    public FenwickTree2D(int[][] arr) {
        int n = arr.length, m = arr[0].length;
        ft = new int[n + 1][m + 1];
        build(arr);
    }

    private int LSOne(int n) {
        return (n & (-n));
    }
    private void build(int[][] arr) {
        for (int i = 0; i < arr.length; i++) {
            for (int j = 0; j < arr[0].length; j++) {
                update(i + 1, j + 1, arr[i][j]);
            }
        }
    }

    public void update(int row, int col, int value) {
        for (int i = row; i < ft.length; i += LSOne(i)) {
            for (int j = col; j < ft[0].length; j += LSOne(j)) {
                ft[i][j] += value;
            }
        }
    }

    private int querySum(int row, int col) {
        int sum = 0;
        for (int i = row; i > 0; i -= LSOne(i)) {
            for (int j = col; j > 0; j -= LSOne(j)) {
                sum += ft[i][j];
            }
        }
        return sum;
    }

    public int rangeSum(int x1, int y1, int x2, int y2) {
        // Inclusion & Exclusion principle
        return querySum(x2, y2) - querySum(x1 - 1, y2) - querySum(x2, y1 - 1) + querySum(x1 - 1, y1 - 1);
    }
}
```

## Complexity Analysis
```
- Time Complexity:
- Space Complexity:
```
