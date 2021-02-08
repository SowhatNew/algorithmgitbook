---
description: Medium
---

# 96 Unique Binary Search Trees

```text
// DP, Recursion + Memo, Recursion
// Given n, how many structurally unique BST's (binary search trees) that store values 1 ... n?
```

## A

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Unique Binary Search Trees.
    Memory Usage: 35.9 MB, less than 32.90% of Java online submissions for Unique Binary Search Trees.
     */
    public int numTrees(int n) {
        int[] result = new int[n+1];
        result[0] = result[1] = 1;
        for (int i = 2; i <= n; i++) {
            for (int j = 1; j <= i; j++) {
                result[i] += result[j-1] * result[i-j];
            }
        }
        return result[n];
    }
}
```

## B

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Unique Binary Search Trees.
    Memory Usage: 35.6 MB, less than 66.12% of Java online submissions for Unique Binary Search Trees.
     */
    public int numTrees(int n) {
        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, 1);
        map.put(1, 1);
        return numTrees(n, map);
    }
    private int numTrees(int n, Map<Integer, Integer> map) {
        if (map.containsKey(n)) {
            return map.get(n);
        }
        int sum = 0;
        for (int i = 1; i <= n; i++) {
            sum += numTrees(i-1, map) * numTrees(n-i, map);
        }
        map.put(n, sum);
        return sum;
    }
}
```

## C

```text
public class Solution {
    /*
    Runtime: 2246 ms, faster than 5.02% of Java online submissions for Unique Binary Search Trees.
    Memory Usage: 35.6 MB, less than 66.12% of Java online submissions for Unique Binary Search Trees.
     */
    public int numTrees(int n) {
        //Constraints:
        //1 <= n <= 19
        return generateTrees(1, n);
    }

    private int generateTrees(int lo, int hi) {
        if (hi <= lo) {
            return 1;
        }
        int sum = 0;
        for (int i = lo; i <= hi; ++i) {
            int leftSubtrees = generateTrees(lo, i - 1);
            int rightSubtrees = generateTrees(i + 1, hi);
            sum += leftSubtrees * rightSubtrees;
        }
        return sum;
    }
}
```

