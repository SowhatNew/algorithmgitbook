---
description: Medium
---

# 145 Binary Tree Postorder Traversal

```text
// Given the root of a binary tree, return the postorder traversal of its nodes' values.
```

## A

```text
class Solution {
	/*
	Runtime: 0 ms, faster than 100.00% of Java online submissions for Binary Tree Postorder Traversal.
	Memory Usage: 37.5 MB, less than 30.54% of Java online submissions for Binary Tree Postorder Traversal.
	*/
    List<Integer> list = new LinkedList<>();
    public List<Integer> postorderTraversal(TreeNode root) {
        dfs(root);
        return list;
    }
    private void dfs(TreeNode root) {
        if (root == null) {return;}        
        dfs(root.left);
        dfs(root.right);
        list.add(root.val);
    }
}
```

## B

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Binary Tree Postorder Traversal.
    Memory Usage: 37.4 MB, less than 45.20% of Java online submissions for Binary Tree Postorder Traversal.
     */
    public List<Integer> postorderTraversal(TreeNode root) {
        return bfsPostorder(root);
    }

    private List<Integer> bfsPostorder(TreeNode root) {
        LinkedList<Integer> list = new LinkedList<>();
        if (root == null) {return list;}

        Deque<TreeNode> stack = new LinkedList<>();
        stack.push(root);
        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            list.addFirst(node.val);
            if(node.left != null) {stack.push(node.left);}
            if(node.right != null) {stack.push(node.right);}
        }
        return list;
    }
}
```

