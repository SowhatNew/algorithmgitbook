---
description: Medium
---

# 94 Binary Tree Inorder Traversal

```text
// Given the root of a binary tree, 
// return the inorder traversal of its nodes' values.
```

```java
public class Solution {
    List<Integer> list = new LinkedList<>();
    public List<Integer> inorderTraversal(TreeNode root) {
        dfs(root);
        return list;
    }

    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Binary Tree Inorder Traversal.
    Memory Usage: 37.2 MB, less than 78.41% of Java online submissions for Binary Tree Inorder Traversal.
     */
    private void dfs(TreeNode root) {
        if (root == null) {return;}
        dfs(root.left);
        list.add(root.val);
        dfs(root.right);
    }

    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Binary Tree Inorder Traversal.
    Memory Usage: 37.3 MB, less than 44.19% of Java online submissions for Binary Tree Inorder Traversal.
     */
    private void bfs(TreeNode root) {
        if (root == null) {return;}
        Deque<TreeNode> stack = new LinkedList<>();
        TreeNode cur = root;
        while (!stack.isEmpty() || cur != null) {
            if (cur != null) {
                stack.push(cur);
                cur = cur.left;
            } else {
                TreeNode node = stack.pop();
                list.add(node.val);
                cur = node.right;
            }
            //////////////
//            while (cur != null) {
//                stack.push(cur);
//                cur = cur.left;
//            }
//            TreeNode node = stack.pop();
//            list.add(node.val);
//            cur = node.right;
            //////////////            
        }
    }
}
```

