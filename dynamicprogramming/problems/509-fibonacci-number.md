---
description: Easy
---

# 509 Fibonacci Number

```text
The Fibonacci numbers, commonly denoted F(n) form a sequence, called the Fibonacci sequence, 
such that each number is the sum of the two preceding ones, starting from 0 and 1. 

That is,
F(0) = 0, F(1) = 1
F(n) = F(n - 1) + F(n - 2), for n > 1.
Given n, calculate F(n).


Example 1:
Input: n = 2
Output: 1
Explanation: F(2) = F(1) + F(0) = 1 + 0 = 1.

Example 2:
Input: n = 3
Output: 2
Explanation: F(3) = F(2) + F(1) = 1 + 1 = 2.

Example 3:
Input: n = 4
Output: 3
Explanation: F(4) = F(3) + F(2) = 2 + 1 = 3.
 

Constraints:
0 <= n <= 30
```

## A

```java
// Recursion Force
class Solution {
    /*
    Runtime: 8 ms, faster than 18.88% of Java online submissions for Fibonacci Number.
    Memory Usage: 35.9 MB, less than 34.73% of Java online submissions for Fibonacci Number.
     */
    public int fib(int n) {
        if (n == 0) {
            return 0;
        } 
        if (n == 1) {
            return 1;
        }
        return fib(n - 1) + fib(n - 2);        
    }
}
```

## B

```java
// Recursion Memo
class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Fibonacci Number.
    Memory Usage: 35.6 MB, less than 72.71% of Java online submissions for Fibonacci Number.
     */
    public int fib(int n) {
        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, 0);
        map.put(1, 1);
        return helper(n, map);
    }
    
    private int helper(final int n, Map<Integer, Integer> map) {
        if (map.containsKey(n)) {
            return map.get(n);
        }
        int result = helper(n - 1, map) + helper(n - 2, map);
        map.put(n, result);
        return result;
    }
}
```

## C

```java
// like DynamicProgramming
class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Fibonacci Number.
    Memory Usage: 35.6 MB, less than 84.13% of Java online submissions for Fibonacci Number.    
    */
    public int fib(int n) {
        if (n == 0) {
            return 0;
        } 
        if (n == 1) {
            return 1;
        }        
        int[] res = new int[n+1];
        res[0] = 0; res[1] = 1;
        for (int i = 2; i <= n; i++) {
            res[i] = res[i-1] + res[i-2];
        }
        return res[n];
    }
}
```

