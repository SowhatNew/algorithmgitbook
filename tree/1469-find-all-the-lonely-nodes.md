---
description: Easy
---

# 1469 Find All the Lonely Nodes

```text
//In a binary tree, a lonely node is a node that is the only child of its parent node.
// The root of the tree is not lonely because it does not have a parent node.
//
//Given the root of a binary tree, return an array containing the values of all lonely nodes in the tree.
// Return the list in any order.
```

```text
public class Solution {
    public List<Integer> getLonelyNodes(TreeNode root) {
        dfs(root);
        return list;
    }
    List<Integer> list = new LinkedList<>();
    private void dfs(TreeNode root) {
        if (root == null) {
            return;
        }
        if (root.left != null && root.right == null) {
            list.add(root.left.val);
        }
        else if (root.left == null && root.right != null) {
            list.add(root.right.val);
        }
        dfs(root.left);
        dfs(root.right);
    }
}
```

