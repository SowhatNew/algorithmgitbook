---
description: Medium
---

# 322 Coin Change

```text
You are given coins of different denominations and a total amount of money amount. 
Write a function to compute the fewest number of coins that you need to make up that amount. 
If that amount of money cannot be made up by any combination of the coins, return -1.

You may assume that you have an infinite number of each kind of coin. 

Example 1:
Input: coins = [1,2,5], amount = 11
Output: 3
Explanation: 11 = 5 + 5 + 1

Example 2:
Input: coins = [2], amount = 3
Output: -1

Example 3:
Input: coins = [1], amount = 0
Output: 0

Example 4:
Input: coins = [1], amount = 1
Output: 1

Example 5:
Input: coins = [1], amount = 2
Output: 2
 

Constraints:
1 <= coins.length <= 12
1 <= coins[i] <= 231 - 1
0 <= amount <= 104
```

## A

```java
public class Solution {
    /*
    Runtime: 11 ms, faster than 88.24% of Java online submissions for Coin Change.
    Memory Usage: 38.7 MB, less than 42.09% of Java online submissions for Coin Change.
     */
    public int coinChange(int[] coins, int amount) {
        int[] res = new int[amount+1];
        res[0] = 0;

        for (int i = 1; i <= amount; i++) {
            int min = Integer.MAX_VALUE;
            for (int coin : coins) {
                int diff = i - coin;
                if (diff < 0 || res[diff] < 0) {
                    continue;
                }
                min = Math.min(min, 1+res[diff]);
            }

            res[i] = (min != Integer.MAX_VALUE) ? min : -1;
        }

        return res[amount];
    }
}
```

## B

```java
public class Solution {
    /*
    Runtime: 157 ms, faster than 5.18% of Java online submissions for Coin Change.
    Memory Usage: 39.9 MB, less than 23.42% of Java online submissions for Coin Change.
     */
    public int coinChange(int[] coins, int amount) {
        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, 0);
        return dp(coins, amount, map);
    }
    private int dp(int[] coins, int amount, Map<Integer, Integer> map) {
        if (map.containsKey(amount)) {
            return map.get(amount);
        }
        if (amount < 0) {
            return -1;
        }

        int min = Integer.MAX_VALUE;
        int sub = 0;
        for (int coin : coins) {
            sub = dp(coins, amount - coin, map);
            if (sub < 0) {
                continue;
            }
            min = Math.min(min, 1+sub);
        }

        if (min != Integer.MAX_VALUE) {
            map.put(amount, min);
            return min;
        } else {
            map.put(amount, -1);
            return -1;
        }
    }
}
```

