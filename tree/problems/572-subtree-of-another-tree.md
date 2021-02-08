---
description: Easy
---

# 572 Subtree of Another Tree

```text
//Given two non-empty binary trees s and t, check whether tree t has exactly
// the same structure and node values with a subtree of s.
// A subtree of s is a tree consists of a node in s and all of this node's descendants.
// The tree s could also be considered as a subtree of itself.
//Given tree s:
//
//     3
//    / \
//   4   5
//  / \
// 1   2
//Given tree t:
//   4
//  / \
// 1   2
//Return true, because t has the same structure and node values with a subtree of s.
```

```text
public class Solution {
    /*
    Runtime: 5 ms, faster than 95.49% of Java online submissions for Subtree of Another Tree.
    Memory Usage: 39.5 MB, less than 23.96% of Java online submissions for Subtree of Another Tree.
     */
    public boolean isSubtree(TreeNode s, TreeNode t) {
        if (s == null || t == null) {return false;}
        if (s.val == t.val) {
            if(isSameTree(s, t)) {return true;}
        }
        return isSubtree(s.left, t) || isSubtree(s.right, t);
    }
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if(p == null && q == null) {return true;}
        if(p == null && q != null) {return false;}
        if(p != null && q == null) {return false;}
        if(p.val != q.val) {return false;}
        return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
    }
}
```

