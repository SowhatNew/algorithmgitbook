---
description: Medium
---

# 503 Next Greater Element II

```text
Given a circular array (the next element of the last element is the first element of the array), 
print the Next Greater Number for every element. 
The Next Greater Number of a number x is the first greater number to its traversing-order next in the array, 
which means you could search circularly to find its next greater number. 
If it doesn't exist, output -1 for this number.

Example 1:
Input: [1,2,1]
Output: [2,-1,2]
Explanation: The first 1's next greater number is 2; 
The number 2 can't find next greater number; 
The second 1's next greater number needs to search circularly, which is also 2.

Note: The length of given array won't exceed 10000.
```

```java
public class Solution {
    /*
    Runtime: 7 ms, faster than 85.06% of Java online submissions for Next Greater Element II.
    Memory Usage: 40.7 MB, less than 59.86% of Java online submissions for Next Greater Element II.
     */
    public int[] nextGreaterElements(int[] nums) {
        int length = nums.length;
        int[] res = new int[nums.length];
        Deque<Integer> stack = new ArrayDeque<>();

        for (int i = 2 * length - 1; i >= 0; i--) {
            while (!stack.isEmpty() && stack.peek() <= nums[i%length]) {
                stack.pop();
            }
            res[i%length] = stack.isEmpty() ? -1 : stack.peek();
            stack.push(nums[i%length]);
        }

        return res;
    }
}
```

