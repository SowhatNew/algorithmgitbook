---
description: Easy
---

# 136 Single Number

```text
Given a non-empty array of integers nums, every element appears twice except for one. 
Find that single one.

Follow up: 
Could you implement a solution with a linear runtime complexity and without using extra memory?

 

Example 1:
Input: nums = [2,2,1]
Output: 1

Example 2:
Input: nums = [4,1,2,1,2]
Output: 4

Example 3:
Input: nums = [1]
Output: 1
 

Constraints:
1 <= nums.length <= 3 * 104
-3 * 104 <= nums[i] <= 3 * 104
Each element in the array appears twice except for one element which appears only once.
```

```java
class Solution {
    /*
    Runtime: 1 ms, faster than 96.29% of Java online submissions for Single Number.
    Memory Usage: 39 MB, less than 80.60% of Java online submissions for Single Number.
     */
    public int singleNumber(int[] nums) {
        int res = 0;
        for (int num : nums) {
            res ^= num;
        }
        return res;
    }
}
```

