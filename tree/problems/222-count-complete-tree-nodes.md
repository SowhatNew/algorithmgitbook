---
description: Medium
---

# 222 Count Complete Tree Nodes

```text
//Given the root of a complete binary tree, 
// return the number of the nodes in the tree.
//
//According to Wikipedia, every level, except possibly the last, 
// is completely filled in a complete binary tree, 
// and all nodes in the last level are as far left as possible. 
// It can have between 1 and 2h nodes inclusive at the last level h.
```

## A

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Count Complete Tree Nodes.
    Memory Usage: 41.5 MB, less than 64.43% of Java online submissions for Count Complete Tree Nodes.
     */
    public int countNodes(TreeNode root) {
        if (root == null) {return 0;}
        return 1 + countNodes(root.left) + countNodes(root.right);
    }
}
```

## B

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Count Complete Tree Nodes.
    Memory Usage: 41.7 MB, less than 40.27% of Java online submissions for Count Complete Tree Nodes.
     */
    public int countNodes(TreeNode root) {
        if (root == null) {return 0;}
        int leftHeight = getHeight(root.left);
        int rightHeight = getHeight(root.right);
        if (leftHeight == rightHeight) {
            // return (1 << leftHeight) - 1  + countNodes(root.right) + 1;
            return (1 << leftHeight) + countNodes(root.right);
        } else {
            // return countNodes(root.left) + 1 + (1 << rightHeight) - 1;
            return countNodes(root.left) + (1 << rightHeight);
        }
    }
    private int getHeight(TreeNode root) {
        if (root == null) {return 0;}
        return 1 + getHeight(root.left);
    }
}
```

## C

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Count Complete Tree Nodes.
    Memory Usage: 41.3 MB, less than 80.77% of Java online submissions for Count Complete Tree Nodes.    
     */
    public int countNodes(TreeNode root) {
        TreeNode left, right;
        left = right = root;
        int hleft, hright;
        hleft = hright = 0;
        while (left != null) {
            hleft++;
            left = left.left;
        }
        while (right != right) {
            hright++;
            right = right.right;
        }
        if (hleft == hright) {
            return (1 << hleft) - 1;
            // return (int)Math.pow(2, hleft) - 1;
        }
        return 1 + countNodes(root.left) + countNodes(root.right);
    }
}
```

