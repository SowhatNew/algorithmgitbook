---
description: Medium
---

# 144 Binary Tree Preorder Traversal

```text
// Given the root of a binary tree, return the preorder traversal of its nodes' values.
```

## A

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Binary Tree Preorder Traversal.
    Memory Usage: 37.4 MB, less than 30.65% of Java online submissions for Binary Tree Preorder Traversal.
     */
    List<Integer> list = new LinkedList<>();
    public List<Integer> preorderTraversal(TreeNode root) {
        dfs(root);
        return list;
    }
    private void dfs(TreeNode root) {
        if (root == null) {return;}
        list.add(root.val);
        dfs(root.left);
        dfs(root.right);
    }
}
```

## B

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Binary Tree Preorder Traversal.
    Memory Usage: 37.3 MB, less than 63.99% of Java online submissions for Binary Tree Preorder Traversal.
     */
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> list = new LinkedList<Integer>();
        if(root==null) {return list;}
        list.add(root.val);
        list.addAll(preorderTraversal(root.left));
        list.addAll(preorderTraversal(root.right));
        return list;
    }
}
```

## C

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Binary Tree Preorder Traversal.
    Memory Usage: 37.1 MB, less than 78.45% of Java online submissions for Binary Tree Preorder Traversal.
    */
    List<Integer> list = new LinkedList<>();
    public List<Integer> preorderTraversal(TreeNode root) {
        bfsPreorder(root);
        return list;
    }
    private void bfsPreorder(TreeNode root) {
        if (root == null) {return;}

        Deque<TreeNode> stack = new LinkedList<>();
        stack.push(root);
        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            list.add(node.val);
            if(node.right!=null) {stack.push(node.right);}
            if(node.left!=null) {stack.push(node.left);}
        }
    }
}
```

