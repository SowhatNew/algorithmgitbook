---
description: Medium
---

# 236 Lowest Common Ancestor of a Binary Tree

```text
Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the definition of LCA on Wikipedia: 
“The lowest common ancestor is defined between two nodes p and q 
as the lowest node in T that has both p and q as descendants 
(where we allow a node to be a descendant of itself).”

Constraints:
The number of nodes in the tree is in the range [2, 105].
-109 <= Node.val <= 109
All Node.val are unique.
p != q
p and q will exist in the tree.
```

## A1

```text
public class Solution {
    /*
    Runtime: 4 ms, faster than 100.00% of Java online submissions for Lowest Common Ancestor of a Binary Tree.
    Memory Usage: 41.2 MB, less than 43.40% of Java online submissions for Lowest Common Ancestor of a Binary Tree.
     */
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null || root == p || root == q) {
            return root;
        }
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        if (left == null) {
            return right;
        }
        if (right == null) {
            return left;
        }
        return root;
    }
}
```

## A2

```text
public class Solution {
    /*
    Runtime: 453 ms, faster than 5.01% of Java online submissions for Lowest Common Ancestor of a Binary Tree.
    Memory Usage: 43.2 MB, less than 14.50% of Java online submissions for Lowest Common Ancestor of a Binary Tree.
     */
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null || root == p || root == q) {
            return root;
        }
        Deque<TreeNode> stack = new LinkedList<>();
        TreeNode cur = root.left;
        boolean pLeft = false;
        boolean pRight = false;
        while (cur != null || !stack.isEmpty()) {
            while (cur != null) {
                stack.push(cur);
                cur = cur.left;
            }
            cur = stack.pop();
            if (cur == p) {
                pLeft = true;
            }
            if (cur == q) {
                pRight = true;
            }
            if (pLeft && pRight) {
                break;
            }
            cur = cur.right;
        }
        if (pLeft && pRight) {
            return lowestCommonAncestor(root.left, p, q);
        }
        if (!pLeft && !pRight) {
            return lowestCommonAncestor(root.right, p, q);
        }
        return root;
    }
}
```

## B

我们可以把从 `root` 到 `p` 和 `root` 到 `q` 的路径找到，例如

`root -> * -> * -> r -> x -> x -> p`

`root -> * -> * -> r -> y -> y -> y -> y -> q`

