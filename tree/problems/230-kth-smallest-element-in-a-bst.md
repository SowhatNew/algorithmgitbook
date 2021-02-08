---
description: Medium
---

# 230 Kth Smallest Element in a BST

```text
Given a binary search tree, write a function kthSmallest to find the kth smallest element in it.
Follow up:
What if the BST is modified (insert/delete operations) often and you need to find the kth smallest frequently? 
How would you optimize the kthSmallest routine?

Constraints:
The number of elements of the BST is between 1 to 10^4.
You may assume k is always valid, 1 ≤ k ≤ BST's total elements.
```

## A

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Kth Smallest Element in a BST.
    Memory Usage: 38.9 MB, less than 64.95% of Java online submissions for Kth Smallest Element in a BST.
     */
    public int kthSmallest(TreeNode root, int k) {
        n = 0;
        res = 0;
        flag = false;
        this.k = k;
        dfs(root);
        return res;
    }
    int n;
    int k;
    int res;
    boolean flag;
    private void dfs(TreeNode root) {
        if (root == null) {return;}
        dfs(root.left);
        if (flag) {return;}
        n++;
        if (n == k) {
            res = root.val;
            flag = true;
            return;
        }
        if (flag) {return;}
        dfs(root.right);
    }
}
```

## B

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Kth Smallest Element in a BST.
    Memory Usage: 38.8 MB, less than 64.95% of Java online submissions for Kth Smallest Element in a BST.
     */
    public int kthSmallest(TreeNode root, int k) {
        int n = nodeCount(root.left);
        if (n + 1 == k) {
            return root.val;
        } else if (n + 1 < k) {
            return kthSmallest(root.right, k - n - 1);
        } else {
            return kthSmallest(root.left, k);
        }
    }
    private int nodeCount(TreeNode root) {
        if (root == null) {return 0;}
        return 1 + nodeCount(root.left) + nodeCount(root.right);
    }
}
```

