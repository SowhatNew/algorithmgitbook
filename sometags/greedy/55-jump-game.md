---
description: Medium
---

# 55 Jump Game

```text
Given an array of non-negative integers nums, 
you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

 

Example 1:
Input: nums = [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.

Example 2:
Input: nums = [3,2,1,0,4]
Output: false
Explanation: You will always arrive at index 3 no matter what. Its maximum jump length is 0, 
which makes it impossible to reach the last index.
 

Constraints:
1 <= nums.length <= 3 * 104
0 <= nums[i] <= 105
```

## A

```java
public class Solution {
    /*
    Runtime: 1 ms, faster than 86.66% of Java online submissions for Jump Game.
    Memory Usage: 40.9 MB, less than 62.43% of Java online submissions for Jump Game.
     */
    public boolean canJump(int[] nums) {
        int n = nums.length;
        int farthest = 0;
        for (int i = 0; i < n - 1; i++) {
            farthest = Math.max(farthest, i + nums[i]);
            if (farthest <= i) {
                return false;
            }
        }
        return true;
    }
}
```

## B

```java
public class Solution {
    /*
    Runtime: 1 ms, faster than 86.66% of Java online submissions for Jump Game.
    Memory Usage: 41.2 MB, less than 43.66% of Java online submissions for Jump Game.
     */
    public boolean canJump(int[] nums) {
        if (nums.length < 2) {
            return true;
        }
        for (int cur = nums.length - 2; cur >= 0; cur--) {
            if (nums[cur] == 0) {
                int neededJumps = 1;
                while (neededJumps > nums[cur]) {
                    neededJumps++;
                    cur--;
                    if (cur < 0) {return false;}
                }
            }
        }
        return true;
    }
}
```

