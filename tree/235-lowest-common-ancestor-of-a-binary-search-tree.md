---
description: Easy
---

# 235 Lowest Common Ancestor of a Binary Search Tree

```text
// Given a binary search tree (BST), find the lowest common ancestor (LCA) of two given nodes in the BST.
// According to the definition of LCA on Wikipedia:
// “The lowest common ancestor is defined between two nodes p and q as the lowest node in T 
// that has both p and q as descendants 
// (where we allow a node to be a descendant of itself).”

// Constraints:
// The number of nodes in the tree is in the range [2, 105].
// -109 <= Node.val <= 109
// All Node.val are unique.
// p != q
// p and q will exist in the BST.
```

## A

```text
class Solution {
    /*
    Runtime: 3 ms, faster than 100.00% of Java online submissions for Lowest Common Ancestor of a Binary Search Tree.
    Memory Usage: 39.6 MB, less than 84.92% of Java online submissions for Lowest Common Ancestor of a Binary Search Tree.
     */
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root==null) {return null;}
        if(p.val<root.val && q.val<root.val) {
            return lowestCommonAncestor(root.left,p,q);
        }
        if(p.val>root.val && q.val>root.val){
            return lowestCommonAncestor(root.right,p,q);
        }
        return root;
    }
}
```

## B

```text
public class Solution {
    /*
    Runtime: 4 ms, faster than 49.84% of Java online submissions for Lowest Common Ancestor of a Binary Search Tree.
    Memory Usage: 39.7 MB, less than 73.40% of Java online submissions for Lowest Common Ancestor of a Binary Search Tree.
     */
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root==null || root==p || root==q) {return root;}

        TreeNode left = lowestCommonAncestor(root.left,p,q);
        TreeNode right = lowestCommonAncestor(root.right,p,q);

        if(left==null) {return right;}
        if(right==null) {return left;}

        return root;
    }
}
```

## C

```text
public class Solution {
    /*
    Runtime: 3 ms, faster than 100.00% of Java online submissions for Lowest Common Ancestor of a Binary Search Tree.
    Memory Usage: 39.6 MB, less than 93.00% of Java online submissions for Lowest Common Ancestor of a Binary Search Tree.
     */
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        while (root != null) {
            if (root.val > p.val && root.val > q.val) {root = root.left;}
            else if (root.val < p.val && root.val < q.val) {root = root.right;}
            else {return root;}
        }
        return root;
    }
}
```

