---
description: Hard
---

# 52\* N-Queens II

```text
The n-queens puzzle is the problem of placing n queens on an n x n chessboard such that no two queens attack each other.

Given an integer n, return the number of distinct solutions to the n-queens puzzle.

Example 1:
Input: n = 4
Output: 2
Explanation: There are two distinct solutions to the 4-queens puzzle as shown.

Example 2:
Input: n = 1
Output: 1
 

Constraints:

1 <= n <= 9
```

```java
class Solution {
    /*
    Runtime: 1 ms, faster than 75.87% of Java online submissions for N-Queens II.
    Memory Usage: 36.2 MB, less than 41.49% of Java online submissions for N-Queens II.
     */
    public int totalNQueens(int n) {
        List<Integer> res = new ArrayList<>();
        backtrack(0, new boolean[n],
                new boolean[2*n], new boolean[2*n], res);
        return res.size();
    }

    private void backtrack(int row, boolean[] cols,
                           boolean[] d1, boolean[] d2, // diagonals
                           List<Integer> res) {
        int length = cols.length;
        if (row == length) {
            res.add(1);
            return;
        }

        for (int col = 0; col < length; col++) {
            int id1 = row - col + length;
            int id2 = 2 * length - row - col - 1;
            if (!cols[col] && !d1[id1] && !d2[id2]) {
                cols[col] = true; d1[id1] = true; d2[id2] = true;
                backtrack(row + 1, cols, d1, d2, res);
                cols[col] = false; d1[id1] = false; d2[id2] = false;
            }
        }
    }
}

```

