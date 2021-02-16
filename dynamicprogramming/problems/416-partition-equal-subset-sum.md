---
description: Medium
---

# 416 Partition Equal Subset Sum

```text
Given a non-empty array nums containing only positive integers, 
find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.


Example 1:
Input: nums = [1,5,11,5]
Output: true
Explanation: The array can be partitioned as [1, 5, 5] and [11].

Example 2:
Input: nums = [1,2,3,5]
Output: false
Explanation: The array cannot be partitioned into equal sum subsets.

Constraints:
1 <= nums.length <= 200
1 <= nums[i] <= 100
```

## A

```java
public class Solution {
    /*
    Runtime: 42 ms, faster than 42.31% of Java online submissions for Partition Equal Subset Sum.
    Memory Usage: 39.9 MB, less than 47.34% of Java online submissions for Partition Equal Subset Sum.
     */
    public boolean canPartition(int[] nums) {
        int sum = Arrays.stream(nums).sum();
        if ((sum & 1) == 1) {
            return false;
        }
        sum /= 2;
        int n = nums.length;

        boolean[][] dp = new boolean[n+1][sum+1];
        for (int i = 0; i <= n; i++) {
            dp[i][0] = true;
        }

        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= sum; j++) {
                if (j - nums[i-1] >= 0) {
                    dp[i][j] = dp[i-1][j] || dp[i-1][j-nums[i-1]];
                } else {
                    dp[i][j] = dp[i-1][j];
                }
            }
        }
        // 1,5,11,5
//        for (int j = -1; j <= sum; j++) {
//            System.out.printf("%3d", j);
//        }
//        for (int i = 0; i <= n; i++) {
//            System.out.printf("\n%2d:", i);
//            for (int j = 0; j <= sum; j++) {
//                System.out.printf("%3d", (dp[i][j] ? 1 : 0));
//            }
//        }
        return dp[n][sum];
    }
}
```

## B

```java
public class Solution {
    /*
    Runtime: 24 ms, faster than 68.06% of Java online submissions for Partition Equal Subset Sum.
    Memory Usage: 38.2 MB, less than 94.45% of Java online submissions for Partition Equal Subset Sum.
     */
    public boolean canPartition(int[] nums) {
        int sum = Arrays.stream(nums).sum();
        if ((sum & 1) == 1) {
            return false;
        }
        sum /= 2;
        int n = nums.length;

        boolean[] dp = new boolean[sum+1];
        dp[0] = true;

        for (int i = 0; i < n; i++) {
            for (int j = sum; j >= 0; j--) {
                if (j - nums[i] >= 0) {
                    dp[j] = dp[j] || dp[j - nums[i]];
                }
            }
        }
        return dp[sum];
    }
}
```

