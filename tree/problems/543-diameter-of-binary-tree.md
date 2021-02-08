---
description: Easy
---

# 543 Diameter of Binary Tree

```text
//Given a binary tree, you need to compute the length of the diameter of the tree.
// The diameter of a binary tree is the length of the longest path between any two nodes in a tree.
// This path may or may not pass through the root.
//Example:
//Given a binary tree
//          1
//         / \
//        2   3
//       / \
//      4   5
//Return 3, which is the length of the path [4,2,1,3] or [5,2,1,3].
//Note: The length of path between two nodes is represented by the number of edges between them.
```

```text
public class Solution {
    // 左右孩子深度相加
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Diameter of Binary Tree.
    Memory Usage: 40.8 MB, less than 5.36% of Java online submissions for Diameter of Binary Tree.
     */
    int num = 0;
    public int diameterOfBinaryTree(TreeNode root) {
        maxDepth(root);
        return num;
    }
    public int maxDepth(TreeNode root) {
        if (root == null) {return 0;}
        int leftDepth = maxDepth(root.left);
        int rightDepth = maxDepth(root.right);
        num = (num > (leftDepth + rightDepth)) ? num : (leftDepth + rightDepth);
        return Math.max(leftDepth, rightDepth) + 1;
    }
}
```

