---
description: Easy
---

# 111 Minimum Depth of Binary Tree

```text
// Given a binary tree, find its minimum depth.
// The minimum depth is the number of nodes along the shortest path 
// from the root node down to the nearest leaf node.
// Note: A leaf is a node with no children.
```

## A

```text
class Solution {
    /**
     * Runtime: 5 ms, faster than 55.25% of Java online submissions for Minimum Depth of Binary Tree.
     * Memory Usage: 60.2 MB, less than 37.11% of Java online submissions for Minimum Depth of Binary Tree.
     */    
    public int minDepth(TreeNode root) {
        if (root == null) {return 0;}
        int leftDepth = minDepth(root.left);
        int rightDepth = minDepth(root.right);
        return (leftDepth == 0 || rightDepth == 0) ?
                leftDepth + rightDepth + 1: Math.min(leftDepth, rightDepth) + 1;
    }
}
```

## B

```text
class Solution{
    /**
     * Runtime: 0 ms, faster than 100.00% of Java online submissions for Minimum Depth of Binary Tree.
     * Memory Usage: 58.6 MB, less than 97.39% of Java online submissions for Minimum Depth of Binary Tree.
     */
    public int minDepth(TreeNode root) {
        if (root == null) {return 0;}

        int depth = 1;
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        while (!q.isEmpty()){
            int size = q.size();
            for (int i = 0; i < size; i++) {
                TreeNode temp = q.poll();
                if (temp.left == null && temp.right == null) {
                    return depth;
                }
                if (temp.left != null) {q.offer(temp.left);}
                if (temp.right != null) {q.offer(temp.right);}
            }
            depth++;
        }
        return depth;
    }
}
```

