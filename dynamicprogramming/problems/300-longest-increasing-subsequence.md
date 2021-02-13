---
description: Medium
---

# 300 Longest Increasing Subsequence

```text
Given an integer array nums, return the length of the longest strictly increasing subsequence.

A subsequence is a sequence that can be derived from an array by deleting some or no elements without changing the order of the remaining elements. 
For example, [3,6,2,7] is a subsequence of the array [0,3,1,6,2,2,7].

 

Example 1:
Input: nums = [10,9,2,5,3,7,101,18]
Output: 4
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4.

Example 2:
Input: nums = [0,1,0,3,2,3]
Output: 4

Example 3:
Input: nums = [7,7,7,7,7,7,7]
Output: 1
 

Constraints:
1 <= nums.length <= 2500
-104 <= nums[i] <= 104
 

Follow up:
Could you come up with the O(n2) solution?
Could you improve it to O(n log(n)) time complexity?
```

## A

```java
public class Solution {
    /*
    Runtime: 59 ms, faster than 48.08% of Java online submissions for Longest Increasing Subsequence.
    Memory Usage: 38.8 MB, less than 50.24% of Java online submissions for Longest Increasing Subsequence.
     */
    public int lengthOfLIS(int[] nums) {
        int[] dp = new int[nums.length];
        Arrays.fill(dp, 1);

        for (int i = 0; i < nums.length; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[j] < nums[i]) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
            }
        }
        
        return Arrays.stream(dp).summaryStatistics().getMax();
    }
}
```

## B

```java
public class Solution {
    /*
    Runtime: 3 ms, faster than 84.10% of Java online submissions for Longest Increasing Subsequence.
    Memory Usage: 38.4 MB, less than 83.89% of Java online submissions for Longest Increasing Subsequence.
     */
    public int lengthOfLIS(int[] nums) {
        int[] top = new int[nums.length];
        int piles = 0;
        for (int i = 0; i < nums.length; i++) {
            int poker = nums[i];
            int left = 0, right = piles;
            while (left < right) {
                int mid = left + (right - left) / 2;
                if (top[mid] > poker) {
                    right = mid;
                } else if (top[mid] < poker) {
                    left = mid + 1;
                } else {
                    right = mid;
                }
            }

            if (left == piles) {
                piles++;
            }
            top[left] = poker;
        }
        return piles;
    }
}
```

