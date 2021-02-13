---
description: Easy
---

# 53 Maximum Subarray

```text
Given an integer array nums, find the contiguous subarray (containing at least one number) 
which has the largest sum and return its sum.


Example 1:
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.

Example 2:
Input: nums = [1]
Output: 1

Example 3:
Input: nums = [0]
Output: 0

Example 4:
Input: nums = [-1]
Output: -1

Example 5:
Input: nums = [-100000]
Output: -100000
 

Constraints:
1 <= nums.length <= 3 * 104
-105 <= nums[i] <= 105
 

Follow up: 
If you have figured out the O(n) solution, 
try coding another solution using the divide and conquer approach, which is more subtle.
```

## A

```java
public class Solution {
    /*
    Runtime: 1 ms, faster than 53.80% of Java online submissions for Maximum Subarray.
    Memory Usage: 39.1 MB, less than 45.46% of Java online submissions for Maximum Subarray.
     */
    public int maxSubArray(int[] nums) {
        int n = nums.length;
        if (n == 0) {
            return 0;
        }

        int cur;
        int pre = nums[0];
        int res = nums[0];
        for (int i = 1; i < n; i++) {
            cur = Math.max(nums[i], nums[i] + pre);
            pre = cur;
            res = Math.max(res, cur);
        }

        return res;
    }
}
```

## B

```java
public class Solution {
    /*
    Runtime: 4 ms, faster than 8.70% of Java online submissions for Maximum Subarray.
    Memory Usage: 39.4 MB, less than 18.99% of Java online submissions for Maximum Subarray.
     */
    public int maxSubArray(int[] nums) {
        int n = nums.length;
        if (n == 0) {
            return 0;
        }

        int[] dp = new int[n];
        dp[0] = nums[0];
        for (int i = 1; i < n; i++) {
            dp[i] = Math.max(nums[i], nums[i] + dp[i-1]);
        }

        return Arrays.stream(dp).summaryStatistics().getMax();
    }
}
```

