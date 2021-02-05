---
description: Easy
---

# 226 Invert Binary Tree

```text
Invert a binary tree.

Example:
Input:

     4
   /   \
  2     7
 / \   / \
1   3 6   9
Output:

     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

## A

```text
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null) {return root;}
        TreeNode temp;
        temp = root.left;
        root.left = root.right;
        root.right = temp;
        if (root.left != null) {invertTree(root.left);}
        if (root.right != null) {invertTree(root.right);}
        return root;
    }
}
```

## B

```text
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null) {return root;}
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        TreeNode temp;
        while (!queue.isEmpty()) {
            TreeNode treeNode = queue.poll();
            temp = treeNode.left;
            treeNode.left = treeNode.right;
            treeNode.right = temp;
            if (treeNode.left != null) {queue.offer(treeNode.left);}
            if (treeNode.right != null) {queue.offer(treeNode.right);}
        }
        return root;
    }
}
```

