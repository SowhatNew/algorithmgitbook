---
description: Hard
---

# 72\* Edit Distance

```text
Given two strings word1 and word2, return the minimum number of operations required to convert word1 to word2.

You have the following three operations permitted on a word:
Insert a character
Delete a character
Replace a character
 

Example 1:
Input: word1 = "horse", word2 = "ros"
Output: 3
Explanation: 
horse -> rorse (replace 'h' with 'r')
rorse -> rose (remove 'r')
rose -> ros (remove 'e')

Example 2:
Input: word1 = "intention", word2 = "execution"
Output: 5
Explanation: 
intention -> inention (remove 't')
inention -> enention (replace 'i' with 'e')
enention -> exention (replace 'n' with 'x')
exention -> exection (replace 'n' with 'c')
exection -> execution (insert 'u')
 

Constraints:
0 <= word1.length, word2.length <= 500
word1 and word2 consist of lowercase English letters.
```

## A1

```java
public class Solution {
    /*
    Runtime: 3 ms, faster than 99.51% of Java online submissions for Edit Distance.
    Memory Usage: 39.8 MB, less than 24.36% of Java online submissions for Edit Distance.
     */
    private int memo[][];
    public int minDistance(String s1, String s2) {
        int m = s1.length(), n = s2.length();
        memo = new int[m][n];
        for (int[] row : memo) {
            Arrays.fill(row, -1);
        }

        return dp(s1, m-1, s2, n-1);
    }

    private int dp(String s1, int i, String s2, int j) {
        int res = -1;
        if (i == -1) {
            return j + 1;
        }
        if (j == -1) {
            return i + 1;
        }

        if (memo[i][j] != -1) {
            return memo[i][j];
        }

        if (s1.charAt(i) == s2.charAt(j)) {
            res = dp(s1, i-1, s2, j-1);
            memo[i][j] = res;
            return res;
        } else {
            res = min(
                    1 + dp(s1, i, s2,j-1), // insert
                    1 + dp(s1, i-1, s2, j), // delete
                    1 + dp(s1, i-1, s2,j-1) // replace
            );
            memo[i][j] = res;
            return res;
        }
    }

    private int min(int a, int b, int c) {
        return Math.min(a, Math.min(b, c));
    }
}
```

## A2

```java
public class Solution {
    /*
    Runtime: 3 ms, faster than 99.51% of Java online submissions for Edit Distance.
    Memory Usage: 39.4 MB, less than 35.17% of Java online submissions for Edit Distance.
     */
    private int memo[][];
    public int minDistance(String s1, String s2) {
        int m = s1.length(), n = s2.length();
        memo = new int[m][n];
        for (int[] row : memo) {
            Arrays.fill(row, -1);
        }

        return dp(s1, 0, s2, 0);
    }

    private int dp(String s1, int i, String s2, int j) {
        int res = -1;
        if (i == s1.length()) {
            return s2.length() - j;
        }
        if (j == s2.length()) {
            return s1.length() - i;
        }

        if (memo[i][j] != -1) {
            return memo[i][j];
        }

        if (s1.charAt(i) == s2.charAt(j)) {
            res = dp(s1, i + 1, s2, j + 1);
            memo[i][j] = res;
            return res;
        } else {
            res = min(
                    1 + dp(s1, i, s2,j+1), // insert
                    1 + dp(s1, i+1, s2, j), // delete
                    1 + dp(s1, i+1, s2,j+1) // replace
            );
            memo[i][j] = res;
            return res;
        }
    }

    private int min(int a, int b, int c) {
        return Math.min(a, Math.min(b, c));
    }
}
```

## B

```java
public class Solution {
    /*
    Runtime: 4 ms, faster than 92.57% of Java online submissions for Edit Distance.
    Memory Usage: 39.3 MB, less than 44.08% of Java online submissions for Edit Distance.
     */
    public int minDistance(String s1, String s2) {
        int m = s1.length(), n = s2.length();
        int[][] dp = new int[m + 1][n + 1];
        dp[0][0] = 0;
        for (int i = 1; i <= m; i++) {
            dp[i][0] = i;
        }
        for (int j = 1; j <= n; j++) {
            dp[0][j] = j;
        }

        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (s1.charAt(i - 1) == s2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    dp[i][j] = min(
                            dp[i][j - 1] + 1, //insert char of s1
                            dp[i - 1][j] + 1, //delete char of s1
                            dp[i - 1][j - 1] + 1 //replace char of s1 with char of s2
                    );
                }
            }
        }

        return dp[m][n];
    }

    private int min(int a, int b, int c) {
        return Math.min(a, Math.min(b, c));
    }
}
```

