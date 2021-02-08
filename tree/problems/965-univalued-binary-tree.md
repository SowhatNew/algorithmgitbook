---
description: Easy
---

# 965 Univalued Binary Tree

```text
// A binary tree is univalued if every node in the tree has the same value.
// Return true if and only if the given tree is univalued.
```

## A

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Univalued Binary Tree.
    Memory Usage: 36.4 MB, less than 69.88% of Java online submissions for Univalued Binary Tree.
     */
    public boolean isUnivalTree(TreeNode root) {
        if (root == null) {return false;}
        return dfs(root, root.val);
    }
    public boolean dfs(TreeNode root, int value) {
        if (root.val != value) {return false;}
        boolean left = true;
        boolean right = true;
        if (root.left != null) {
            left = dfs(root.left, value);}
        if (root.right != null) {
            right = dfs(root.right, value);
        }
        return left && right;
    }
}
```

## B

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Univalued Binary Tree.
    Memory Usage: 36.5 MB, less than 69.88% of Java online submissions for Univalued Binary Tree.
     */
    public boolean isUnivalTree(TreeNode root) {
        return dfs(root , root.val);
    }
    public boolean dfs(TreeNode root , int val){
        if(root == null) {return true;}

        return root.val == val &&
                dfs(root.left,val) &&
                dfs(root.right,val);
    }
}
```

