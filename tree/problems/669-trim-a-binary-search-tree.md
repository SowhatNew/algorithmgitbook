---
description: Easy
---

# 669 Trim a Binary Search Tree

```text
//Given the root of a binary search tree and the lowest and highest boundaries as low and high,
// trim the tree so that all its elements lies in [low, high]. 
// Trimming the tree should not change the relative structure of the elements that will remain in the tree 
// (i.e., any node's descendant should remain a descendant). 
// It can be proven that there is a unique answer.
//Return the root of the trimmed binary search tree. 
// Note that the root may change depending on the given bounds.
```

## A

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Trim a Binary Search Tree.
    Memory Usage: 38.8 MB, less than 40.61% of Java online submissions for Trim a Binary Search Tree.
     */
    public TreeNode trimBST(TreeNode root, int low, int high) {
        if (root == null) {
            return null;
        }

        while (root.val < low || root.val > high) {
            if (root.val < low) {
                root = root.right;
            }
            if (root.val > high) {
                root = root.left;
            }
        }

        Deque<TreeNode> stack = new LinkedList<>();
        stack.push(root);
        boolean adjusted = false;

        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();

            if (node.left != null && node.left.val < low) {
                node.left = node.left.right;
                adjusted = true;
            }
            if (node.right != null && node.right.val > high) {
                node.right = node.right.left;
                adjusted = true;
            }
            if (!adjusted) {
                if (node.left != null) {
                    stack.push(node.left);
                }
                if (node.right != null) {
                    stack.push(node.right);
                }
            } else {
                stack.push(node);
            }
            adjusted = false;
        }
        return root;
    }
}
```

## B

```text
class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Trim a Binary Search Tree.
    Memory Usage: 38.6 MB, less than 70.12% of Java online submissions for Trim a Binary Search Tree.
     */
    public TreeNode trimBST(TreeNode root, int low, int high) {
        if (root == null) {return null;}
        if (root.val < low) {
            return trimBST(root.right, low, high);
        }else if (root.val > high) {
            return trimBST(root.left, low, high);
        }
        root.left = trimBST(root.left, low, high);
        root.right = trimBST(root.right, low, high);
        return root;
    }
}
```

