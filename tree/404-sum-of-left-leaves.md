---
description: Easy
---

# 404 Sum of Left Leaves

```text
//Find the sum of all left leaves in a given binary tree.
//
//Example:
//
//    3
//   / \
//  9  20
//    /  \
//   15   7
//
//There are two left leaves in the binary tree, with values 9 and 15 respectively. Return 24.
```

## A

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Sum of Left Leaves.
    Memory Usage: 37 MB, less than 17.72% of Java online submissions for Sum of Left Leaves.
     */
    public int sumOfLeftLeaves(TreeNode root) {
        if (root == null) {return 0;}
        return (root.left != null && root.left.left == null && root.left.right == null ? root.left.val : 0)
                + sumOfLeftLeaves(root.left) + sumOfLeftLeaves(root.right);
    }
}
```

## B

```text
class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Sum of Left Leaves.
    Memory Usage: 36.6 MB, less than 78.07% of Java online submissions for Sum of Left Leaves.
     */
    public int sumOfLeftLeaves(TreeNode root) {
        if (root == null) {return 0;}
        return dfs(root.left, true) + dfs(root.right, false);
    }
    private int dfs(TreeNode root, boolean isLeft) {
        if (root == null) {return 0;}
        if (isLeft && root.left == null && root.right == null) {return root.val;}
        return dfs(root.left, true) + dfs(root.right, false);
    }

}
```

## C

```text
public class Solution {
    /*
    Runtime: 1 ms, faster than 5.58% of Java online submissions for Sum of Left Leaves.
    Memory Usage: 36.5 MB, less than 88.89% of Java online submissions for Sum of Left Leaves.
     */
    public int sumOfLeftLeaves(TreeNode root) {
        if (root == null) {return 0;}
        Deque<TreeNode> stack = new LinkedList<>();
        stack.push(root);
        int sum = 0;
        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            if (node == null) {continue;}
            if (node.left != null && node.left.left == null && node.left.right == null) {
                sum += node.left.val;
            }
            stack.push(node.left);
            stack.push(node.right);
        }
        return sum;
    }
}
```

