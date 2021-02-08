---
description: Medium
---

# 98 Validate Binary Search Tree

```text
//Given the root of a binary tree, determine if it is a valid binary search tree (BST).
//A valid BST is defined as follows:
//The left subtree of a node contains only nodes with keys less than the node's key.
//The right subtree of a node contains only nodes with keys greater than the node's key.
//Both the left and right subtrees must also be binary search trees.
```

## A

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Validate Binary Search Tree.
    Memory Usage: 38.4 MB, less than 81.73% of Java online submissions for Validate Binary Search Tree.
     */
    public boolean isValidBST(TreeNode root) {
        return dfs(root, null, null);
    }
    private boolean dfs(TreeNode root, Integer min, Integer max) {
        if (root == null) {return true;}
        if (min != null && root.val <= min){
            return false;
        }
        if (max != null && root.val >= max) {
            return false;
        }
        return dfs(root.left, min, root.val) &&
                dfs(root.right, root.val, max);
    }
}
```

## B

```text
public class Solution {
    /*
    Runtime: 2 ms, faster than 9.62% of Java online submissions for Validate Binary Search Tree.
    Memory Usage: 39.1 MB, less than 18.76% of Java online submissions for Validate Binary Search Tree.     */
    public boolean isValidBST(TreeNode root) {
        return bfsInorder(root);
    }

    private boolean bfsInorder(TreeNode root) {
        if (root == null) {return true;}

        List<Integer> list = new LinkedList<>();
        Deque<TreeNode> stack = new LinkedList<>();
        TreeNode cur = root;
        while (!stack.isEmpty() || cur != null) {
            /////////////
            if (cur != null) {
                stack.push(cur);
                cur = cur.left;
            } else {
                TreeNode node = stack.pop();
                if (list.size() > 0 && list.get(list.size()-1) >= node.val) {
                    return false;
                }
                list.add(node.val);
                cur = node.right;
            }
            /////////////
//            while (cur != null) {
//                stack.push(cur);
//                cur = cur.left;
//            }
//            TreeNode node = stack.pop();
//            if (list.size() > 0 && list.get(list.size()-1) >= node.val) {
//                return false;
//            }
//            list.add(node.val);
//            cur = node.right;            
        }
        return true;
    }
}
```

