---
description: Medium
---

# 739 Daily Temperatures

```text
Given a list of daily temperatures T, return a list such that, for each day in the input, 
tells you how many days you would have to wait until a warmer temperature. 
If there is no future day for which this is possible, put 0 instead.

For example, given the list of temperatures T = [73, 74, 75, 71, 69, 72, 76, 73], 
your output should be [1, 1, 4, 2, 1, 1, 0, 0].

Note: The length of temperatures will be in the range [1, 30000]. 
Each temperature will be an integer in the range [30, 100].
```

```java
public class Solution {
    /*
    Runtime: 12 ms, faster than 90.92% of Java online submissions for Daily Temperatures.
    Memory Usage: 46.7 MB, less than 95.20% of Java online submissions for Daily Temperatures.
     */
    public int[] dailyTemperatures(int[] T) {
        int[] res = new int[T.length];
        Deque<Integer> stack = new ArrayDeque<>();

        for (int i = T.length - 1; i >= 0; i--) {
            while (!stack.isEmpty() && T[stack.peek()] <= T[i]) {
                stack.pop();
            }
            res[i] = stack.isEmpty() ? 0 : (stack.peek() - i);
            stack.push(i);
        }

        return res;
    }
}
```

