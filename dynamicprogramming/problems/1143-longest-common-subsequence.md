---
description: Medium
---

# 1143 Longest Common Subsequence

```text
Given two strings text1 and text2, return the length of their longest common subsequence.

A subsequence of a string is a new string generated from the original string 
with some characters(can be none) deleted without changing the relative order of the remaining characters. 
(eg, "ace" is a subsequence of "abcde" while "aec" is not). 
A common subsequence of two strings is a subsequence that is common to both strings.


If there is no common subsequence, return 0.


Example 1:
Input: text1 = "abcde", text2 = "ace" 
Output: 3  
Explanation: The longest common subsequence is "ace" and its length is 3.

Example 2:
Input: text1 = "abc", text2 = "abc"
Output: 3
Explanation: The longest common subsequence is "abc" and its length is 3.

Example 3:
Input: text1 = "abc", text2 = "def"
Output: 0
Explanation: There is no such common subsequence, so the result is 0.
 

Constraints:
1 <= text1.length <= 1000
1 <= text2.length <= 1000
The input strings consist of lowercase English characters only.
```

## A

```java
public class Solution {
    /*
    Runtime: 9 ms, faster than 83.65% of Java online submissions for Longest Common Subsequence.
    Memory Usage: 42.8 MB, less than 52.89% of Java online submissions for Longest Common Subsequence.
     */
    public int longestCommonSubsequence(String s1, String s2) {
        int m = s1.length(), n = s2.length();
        int[][] dp = new int[m + 1][n + 1];
        Arrays.fill(dp[0], 0);
        for (int i = 0; i < m; i++) {
            dp[i][0] = 0;
        }

        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (s1.charAt(i - 1) == s2.charAt(j - 1)) {
                    dp[i][j] = 1 + dp[i - 1][j - 1];
                } else {
                    dp[i][j] = Math.max(dp[i][j - 1], dp[i - 1][j]);
                }
            }
        }

        return dp[m][n];
    }
}
```

## B1

```java
public class Solution {
    /*
    Runtime: 14 ms, faster than 38.65% of Java online submissions for Longest Common Subsequence.
    Memory Usage: 42.9 MB, less than 42.74% of Java online submissions for Longest Common Subsequence.
     */
    
    int[][] memo;

    public int longestCommonSubsequence(String text1, String text2) {
        int m = text1.length(), n = text2.length();
        memo = new int[m][n];
        for (int[] row : memo) {
            Arrays.fill(row, -1);
        }

        return dp(text1, m - 1, text2, n - 1);
    }

    private int dp(String s1, int i, String s2, int j) {
        if (i == -1 || j == -1) {
            return 0;
        }

        if (memo[i][j] != -1) {
            return memo[i][j];
        }

        if (s1.charAt(i) == s2.charAt(j)) {
            memo[i][j] = 1 + dp(s1, i - 1, s2, j - 1);
        } else {
            memo[i][j] = Math.max(
                    dp(s1, i - 1, s2, j),
                    dp(s1, i, s2, j - 1)
            );
        }

        return memo[i][j];
    }
}
```

## B2

```java
public class Solution {
    /*
    Runtime: 15 ms, faster than 36.57% of Java online submissions for Longest Common Subsequence.
    Memory Usage: 43.3 MB, less than 21.32% of Java online submissions for Longest Common Subsequence.
     */
    int[][] memo;
    public int longestCommonSubsequence(String text1, String text2) {
        int m = text1.length(), n = text2.length();
        memo = new int[m][n];
        for (int[] row : memo) {
            Arrays.fill(row, -1);
        }
        return dp(text1, 0, text2, 0);
    }

    private int dp(String s1, int i, String s2, int j) {
        if (i == s1.length() || j == s2.length()) {
            return 0;
        }

        if (memo[i][j] != -1) {
            return memo[i][j];
        }

        if (s1.charAt(i) == s2.charAt(j)) {
            memo[i][j] = 1 + dp(s1, i + 1, s2, j + 1);
        } else {
            memo[i][j] = Math.max(
                    dp(s1, i + 1, s2, j),
                    dp(s1, i, s2, j + 1)
            );
        }

        return memo[i][j];
    }
}
```

