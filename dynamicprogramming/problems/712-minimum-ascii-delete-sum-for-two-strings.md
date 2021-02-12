---
description: Medium
---

# 712 Minimum ASCII Delete Sum for Two Strings

```text
Given two strings s1, s2, find the lowest ASCII sum of deleted characters to make two strings equal.

Example 1:
Input: s1 = "sea", s2 = "eat"
Output: 231
Explanation: Deleting "s" from "sea" adds the ASCII value of "s" (115) to the sum.
Deleting "t" from "eat" adds 116 to the sum.
At the end, both strings are equal, and 115 + 116 = 231 is the minimum sum possible to achieve this.

Example 2:
Input: s1 = "delete", s2 = "leet"
Output: 403
Explanation: Deleting "dee" from "delete" to turn the string into "let",
adds 100[d]+101[e]+101[e] to the sum.  Deleting "e" from "leet" adds 101[e] to the sum.
At the end, both strings are equal to "let", and the answer is 100+101+101+101 = 403.
If instead we turned both strings into "lee" or "eet", we would get answers of 433 or 417, which are higher.

Note:
0 < s1.length, s2.length <= 1000.
All elements of each string will have an ASCII value in [97, 122].
```

## A1

```java
public class Solution {
    /*
    Runtime: 26 ms, faster than 42.70% of Java online submissions for Minimum ASCII Delete Sum for Two Strings.
    Memory Usage: 39.6 MB, less than 53.33% of Java online submissions for Minimum ASCII Delete Sum for Two Strings.
     */
    int memo[][];

    public int minimumDeleteSum(String s1, String s2) {
        int m = s1.length(), n = s2.length();
        memo = new int[m][n];
        for (int[] row : memo) {
            Arrays.fill(row, -1);
        }
        return dp(s1, m-1, s2, n-1);
    }

    private int dp(String s1, int i, String s2, int j) {
        int res = 0;
        if (i == -1) {
            for (; j >= 0; j--) {
                res += s2.charAt(j);
            }
            return res;
        }
        if (j == -1) {
            for (; i >= 0; i--) {
                res += s1.charAt(i);
            }
            return res;
        }

        if (memo[i][j] != -1) {
            return memo[i][j];
        }

        if (s1.charAt(i) == s2.charAt(j)) {
            memo[i][j] = dp(s1, i-1, s2, j-1);
        } else {
            memo[i][j] = Math.min(
                    s1.charAt(i) + dp(s1, i-1, s2, j),
                    s2.charAt(j) + dp(s1, i, s2, j-1)
            );
        }

        return memo[i][j];
    }
}
```

## A2

```java
public class Solution {
    /*
    Runtime: 31 ms, faster than 29.48% of Java online submissions for Minimum ASCII Delete Sum for Two Strings.
    Memory Usage: 40.1 MB, less than 26.73% of Java online submissions for Minimum ASCII Delete Sum for Two Strings.
     */
    int memo[][];

    public int minimumDeleteSum(String s1, String s2) {
        int m = s1.length(), n = s2.length();
        memo = new int[m][n];
        for (int[] row : memo) {
            Arrays.fill(row, -1);
        }
        return dp(s1, 0, s2, 0);
    }

    private int dp(String s1, int i, String s2, int j) {
        int res = 0;
        if (i == s1.length()) {
            for (; j < s2.length(); j++) {
                res += s2.charAt(j);
            }
            return res;
        }
        if (j == s2.length()) {
            for (; i < s1.length(); i++) {
                res += s1.charAt(i);
            }
            return res;
        }

        if (memo[i][j] != -1) {
            return memo[i][j];
        }

        if (s1.charAt(i) == s2.charAt(j)) {
            memo[i][j] = dp(s1, i+1, s2, j+1);
        } else {
            memo[i][j] = Math.min(
                    s1.charAt(i) + dp(s1, i+1, s2, j),
                    s2.charAt(j) + dp(s1, i, s2, j+1)
            );
        }

        return memo[i][j];
    }
}
```

## B

```java
public class Solution {
    /*
    Runtime: 18 ms, faster than 75.72% of Java online submissions for Minimum ASCII Delete Sum for Two Strings.
    Memory Usage: 39.2 MB, less than 90.61% of Java online submissions for Minimum ASCII Delete Sum for Two Strings.
     */
    public int minimumDeleteSum(String s1, String s2) {
        int m = s1.length(), n = s2.length();
        int[][] dp = new int[m + 1][n + 1];
        dp[0][0] = 0;
        for (int i = 0; i < s1.length(); i++) {
            dp[i+1][0] = dp[i][0] + s1.charAt(i);
        }
        for (int i = 0; i < s2.length(); i++) {
            dp[0][i+1] = dp[0][i] + s2.charAt(i);
        }

        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (s1.charAt(i-1) == s2.charAt(j-1)) {
                    dp[i][j] = dp[i-1][j-1];
                } else {
                    dp[i][j] = Math.min(
                            s2.charAt(j-1) + dp[i][j-1],
                            s1.charAt(i-1) + dp[i-1][j]
                    );
                }
            }
        }

        return dp[m][n];
    }
}
```

