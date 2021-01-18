---
description: Medium
---

# 129 Sum Root to Leaf Numbers

```text
//Given a binary tree containing digits from 0-9 only, each root-to-leaf path could represent a number.
//
//An example is the root-to-leaf path 1->2->3 which represents the number 123.
//
//Find the total sum of all root-to-leaf numbers.
//
//Note: A leaf is a node with no children.
```

## A

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Sum Root to Leaf Numbers.
    Memory Usage: 38.3 MB, less than 13.45% of Java online submissions for Sum Root to Leaf Numbers.
     */
    int res;
    public int sumNumbers(TreeNode root) {
        res = 0;
        dfs(root, 0);
        return res;
    }
    private void dfs(TreeNode root, int curSum) {
        if (root == null) {return;}
        curSum = curSum * 10 + root.val;
        if (root.left == null && root.right == null) {
            res += curSum;
            return;
        }
        dfs(root.left, curSum);
        dfs(root.right, curSum);
    }


}
```

## B

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Sum Root to Leaf Numbers.
    Memory Usage: 36.6 MB, less than 57.96% of Java online submissions for Sum Root to Leaf Numbers.
     */
    public int sumNumbers(TreeNode root) {
        if (root == null) {
            return 0;
        }
        return dfs(root, 0);
    }
    private int dfs(TreeNode root, int sum) {
        int cursum = sum * 10 + root.val;
        if (root.left == null && root.right == null) {
            return cursum;
        }
        int ans = 0;
        if (root.left != null) {
            ans += dfs(root.left, cursum);
        }
        if (root.right != null) {
            ans += dfs(root.right, cursum);
        }
        return ans;
    }

}
```

## C

```text
public class Solution {
    /*
    Runtime: 2 ms, faster than 13.00% of Java online submissions for Sum Root to Leaf Numbers.
    Memory Usage: 38.7 MB, less than 7.52% of Java online submissions for Sum Root to Leaf Numbers.
     */
    public int sumNumbers(TreeNode root) {
        if (root == null) {return 0;}
        int res = 0;
        int curSum = 0;
        Deque<TreeNode> stack = new LinkedList<>();
        TreeNode cur = root;
        TreeNode pre = null;
        while (cur != null || !stack.isEmpty()) {
            while (cur != null) {
                curSum = curSum * 10 + cur.val;
                stack.push(cur);
                cur = cur.left;
            }
            cur = stack.peek();
            if (cur.left == null && cur.right == null) {
                res += curSum;
            }
            if (cur.right == null || cur.right == pre) {
                curSum = (curSum - cur.val) / 10;
                stack.pop();
                pre = cur;
                cur = null;
            } else {
                cur = cur.right;
            }
        }
        return res;
    }
}
```

