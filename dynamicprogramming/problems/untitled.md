# knapsack

```java
public class Solution {
    /*
    The knapsack problem is a problem in combinatorial optimization:
    Given a set of items, each with a weight and a value,
    determine the number of each item to include in a collection
    so that the total weight is less than or equal to a given limit
    and the total value is as large as possible.
     */
    // 一个可装载重量为W的背包和N个物品，每个物品有重量和价值两个属性。
    // 其中第i个物品的重量为wt[i]，价值为val[i]
    public int knapsack(final int W, int[] wt, int[] val) {
        final int N = wt.length;
        int[][] dp = new int[N+1][W+1];
        for (int i = 1; i <= N; i++) {
            for (int w = 1; w <= W; w++) {
                if (w - wt[i-1] < 0) {
                    dp[i][w] = dp[i-1][w];
                } else {
                    dp[i][w] = Math.max(dp[i-1][w-wt[i-1]] + val[i-1],
                                        dp[i-1][w]);
                }
            }
        }
        return dp[N][W];
    }

    public static void main(String[] args) {
        int W = 4;
        int[] wt = new int[]{2, 1, 3},
              val = new int[]{4, 2, 3};
        
    }
}
```

