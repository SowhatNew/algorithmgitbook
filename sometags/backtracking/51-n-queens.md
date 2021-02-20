---
description: Hard
---

# 51\* N-Queens

```text
The n-queens puzzle is the problem of placing n queens on an n x n chessboard such that no two queens attack each other.

Given an integer n, return all distinct solutions to the n-queens puzzle.

Each solution contains a distinct board configuration of the n-queens' placement, where 'Q' and '.' 
both indicate a queen and an empty space, respectively.

Example 1:
Input: n = 4
Output: [[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]
Explanation: There exist two distinct solutions to the 4-queens puzzle as shown above

Example 2:
Input: n = 1
Output: [["Q"]]
 

Constraints:
1 <= n <= 9
```

## A

```java
class Solution {
    /*
    Runtime: 1 ms, faster than 99.72% of Java online submissions for N-Queens.
    Memory Usage: 39.4 MB, less than 54.98% of Java online submissions for N-Queens.
     */
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> res = new ArrayList<>();
        backtrack(0, new boolean[n],
                new boolean[2*n], new boolean[2*n],
                new String[n], res);
        return res;
    }

    private void backtrack(int rowIndex, boolean[] cols,
                           boolean[] d1, boolean[] d2, // diagonals
                           String[] board, List<List<String>> res) {
        if (rowIndex == board.length) {
            res.add(Arrays.asList(board.clone()));
            return;
        }
        // 0 -1 -2 -3
        // 1 xx xx xx
        // 2 xx xx xx
        // 3 xx xx xx
        for (int col = 0; col < board.length; col++) {
            // top-left to bottom-right
            // rowIndex - col; 1-n ~ n-1
            // rowIndex - col + board.length; 1 ~ 2n-1
            int id1 = rowIndex - col + board.length;
            // bottom-left to top-right
            // rowIndex + col;  0 ~ 2n-2
            // - rowIndex - col - 1;  1-2n ~ -1
            // 2 * board.length - rowIndex - col - 1;  1 ~ 2n-1
            int id2 = 2 * board.length - rowIndex - col - 1;

            if (!cols[col] && !d1[id1] && !d2[id2]) {
                char[] row = new char[board.length];
                Arrays.fill(row, '.');
                row[col] = 'Q';
                board[rowIndex] = new String(row);
                cols[col] = true; d1[id1] = true; d2[id2] = true;
                backtrack(rowIndex + 1, cols, d1, d2, board, res);
                cols[col] = false; d1[id1] = false; d2[id2] = false;
            }
        }
    }
}
```

## B

```java
class Solution {
    /*
    Runtime: 3 ms, faster than 76.02% of Java online submissions for N-Queens.
    Memory Usage: 39.7 MB, less than 32.26% of Java online submissions for N-Queens.
     */
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> res = new ArrayList<>();

        String[] board = new String[n];
        char[] row = new char[n];
        Arrays.fill(row, '.');
        Arrays.fill(board, new String(row));

        backtrack(board, 0, res);
        return res;
    }

    private void backtrack(String[] board, int row, List<List<String>> res) {
        final int length = board.length;

        if (row == length) {
            res.add(Arrays.asList(board.clone()));
            return;
        }

        for (int col = 0; col < length; col++) {
            if (!isValid(board, row, col)) {
                continue;
            }

            char[] temp = board[row].toCharArray();
            temp[col] = 'Q';
            board[row] = new String(temp);

            backtrack(board, row + 1, res);

            temp[col] = '.';
            board[row] = new String(temp);
        }
    }

    private boolean isValid(String[] board, int row, int col) {
        int n = board.length;

        for (int i = 0; i < n; i++) {
            if (board[i].charAt(col) == 'Q') {
                return false;
            }
        }

        for (int i = row - 1, j = col + 1;
             i >= 0 && j < n; i--, j++) {
            if (board[i].charAt(j) == 'Q') {
                return false;
            }
        }

        for (int i = row - 1, j = col - 1;
             i >= 0 && j >= 0; i--, j--) {
            if (board[i].charAt(j) == 'Q') {
                return false;
            }
        }

        return true;
    }
}

```

