---
description: Easy
---

# 104 Maximum Depth of Binary Tree

```text
Given the root of a binary tree, return its maximum depth.
A binary tree's maximum depth is the number of nodes along the longest path 
from the root node down to the farthest leaf node.
```

## A

```text
public class Solution {
	/*
	Runtime: 0 ms, faster than 100.00% of Java online submissions for Maximum Depth of Binary Tree.
	Memory Usage: 39.4 MB, less than 15.10% of Java online submissions for Maximum Depth of Binary Tree.
	 */
    public int maxDepth(TreeNode root) {
        if (root == null) return 0;
        return helper(root, 1);
    }
    public int helper(TreeNode node, int d) {
        if (node.left == null && node.right == null) return d;
        if (node.left == null) return helper(node.right, d + 1);
        if (node.right == null) return helper(node.left, d + 1);
        return Math.max(helper(node.left, d + 1), helper(node.right, d + 1));
    }
}
```

## B

```text
public class Solution {
	/*
	Runtime: 0 ms, faster than 100.00% of Java online submissions for Maximum Depth of Binary Tree.
	Memory Usage: 40.2 MB, less than 5.18% of Java online submissions for Maximum Depth of Binary Tree.
	*/
    public int maxDepth(TreeNode root) {
        if (root == null) {return 0;}
        int leftDepth = maxDepth(root.left);
        int rightDepth = maxDepth(root.right);
        return Math.max(leftDepth, rightDepth) + 1;
    }
}
```

## C

```text
public class Solution {
    /**
    Runtime: 1 ms, faster than 11.59% of Java online submissions for Maximum Depth of Binary Tree.
    Memory Usage: 38.4 MB, less than 99.75% of Java online submissions for Maximum Depth of Binary Tree.
     */
    public int maxDepth(TreeNode root) {
        if (root == null) {return 0;}

        int depth = 0;
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);

        while(!q.isEmpty()){
            int size = q.size();
            for(int i = 0;  i < size; i++){
                TreeNode node = q.poll();
                if(node.left!=null) {q.add(node.left);}
                if(node.right!=null) {q.add(node.right);}
            }
            depth++;
        }
        return depth;
    }
}

```

