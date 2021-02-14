---
description: Medium
---

# 516 Longest Palindromic Subsequence

```text
Given a string s, find the longest palindromic subsequence's length in s. 
You may assume that the maximum length of s is 1000.

Example 1:
Input:
"bbbab"
Output:
4
One possible longest palindromic subsequence is "bbbb".
 
Example 2:
Input:
"cbbd"
Output:
2
One possible longest palindromic subsequence is "bb".
 

Constraints:
1 <= s.length <= 1000
s consists only of lowercase English letters.
```

```java
public class Solution {
    /*
    Runtime: 31 ms, faster than 83.20% of Java online submissions for Longest Palindromic Subsequence.
    Memory Usage: 49.3 MB, less than 55.17% of Java online submissions for Longest Palindromic Subsequence.
     */
    public int longestPalindromeSubseq(String s) {
        int n = s.length();
        int dp[][] = new int[n][n];
        for (int i = 0; i < n; i++) {
            dp[i][i] = 1;
        }
        for (int i = n - 1; i >= 0; i--) {
            for (int j = i + 1; j < n; j++) {
                if (s.charAt(i) == s.charAt(j)) {
                    dp[i][j] = dp[i+1][j-1] + 2;
                } else {
                    dp[i][j] = Math.max(dp[i+1][j], dp[i][j-1]);
                }
            }
        }

//        // bbbab
//        int indexI = -n, indexJ = -n-1;
//        for (int i = -1; i < n; i++) {
//            System.out.printf("%4d", indexJ++);
//        }
//        System.out.println();
//        for (int i = 0; i < n; i++) {
//            System.out.printf("%4d", indexI++);
//            for (int j = 0; j < n; j++) {
//                System.out.printf("%4d", dp[i][j]);
//            }
//            System.out.println();
//        }

        return dp[0][n-1];
    }
}
```

