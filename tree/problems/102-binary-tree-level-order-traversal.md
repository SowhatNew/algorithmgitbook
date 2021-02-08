---
description: Medium
---

# 102 Binary Tree Level Order Traversal

```text
Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).
```

## A

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Binary Tree Level Order Traversal.
    Memory Usage: 39.1 MB, less than 81.62% of Java online submissions for Binary Tree Level Order Traversal.
     */
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> result = new LinkedList<>();
        if (root == null) {return result;}

        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            int size = queue.size();
            List<Integer> tempList = new LinkedList<>();
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                tempList.add(node.val);
                if (node.left != null) {queue.offer(node.left);}
                if (node.right != null) {queue.offer(node.right);}
            }
            result.add(tempList);
        }
        return result;
    }
}
```

## B

```text
public class Solution {
    /*
    Runtime: 1 ms, faster than 55.39% of Java online submissions for Binary Tree Level Order Traversal.
    Memory Usage: 39.4 MB, less than 28.04% of Java online submissions for Binary Tree Level Order Traversal.
     */
    public List<List<Integer>> levelOrder(TreeNode root) {
        dfs(root, 0);
        return result;
    }
    List<List<Integer>> result = new LinkedList<>();
    private void dfs(TreeNode root, int depth) {
        if (root == null) {return;}
        if (result.size() == depth) {
            result.add(new LinkedList<>());
        }
        result.get(depth).add(root.val);
        dfs(root.left, depth+1);
        dfs(root.right, depth+1);
    }
}
```

