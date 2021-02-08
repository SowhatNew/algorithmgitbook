---
description: Easy
---

# 110 Balanced Binary Tree

```text
// Given a binary tree, determine if it is height-balanced.
// For this problem, a height-balanced binary tree is defined as:
// a binary tree in which the left and right subtrees of every node differ in height by no more than 1.

// The number of nodes in the tree is in the range [0, 5000].
// -104 <= Node.val <= 104
```

## A

```text
class Solution {
    public boolean isBalanced(TreeNode root){
        return height(root) < 0 ? false : true;
    }
    public int height(TreeNode root){
        if(root == null) return 0;
        int leftHeight = height(root.left);
        int rightHeight = height(root.right);
        if(leftHeight == -1 || 
            rightHeight == -1 || 
            Math.abs(leftHeight - rightHeight) > 1){
                return -1;
            }
        return Math.max(leftHeight, rightHeight) + 1;
    }
}
```

## B

```text
class Solution2 {
    public boolean isBalanced(TreeNode root) {
        if(root == null) return true;
        else{
            return 
            Math.abs(height(root.left) - height(root.right)) > 1 ? 
            false : 
            true && (isBalanced(root.left) && isBalanced(root.right));
        }
    }
    private int height(TreeNode root){
        if(root == null) return 0;
        int left = 0, right = 0;
        if(root.left != null)
            left = height(root.left);
        if(root.right != null)
            right = height(root.right);
        return Math.max(left, right) + 1;
    }
}
```

