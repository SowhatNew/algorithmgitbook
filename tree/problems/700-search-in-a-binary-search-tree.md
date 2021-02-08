---
description: Easy
---

# 700 Search in a Binary Search Tree

```text
//Given the root node of a binary search tree (BST) and a value. //You need to find the node in the BST that the node's value equals the given value. 
//Return the subtree rooted with that node. 
//If such node doesn't exist, you should return NULL.
```

## A

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Search in a Binary Search Tree.
    Memory Usage: 39 MB, less than 99.57% of Java online submissions for Search in a Binary Search Tree.
     */
    public TreeNode searchBST(TreeNode root, int val) {
        if (root == null) {return null;}
        if (root.val == val) {return root;}
        TreeNode node;
        if (root.val < val) {node = searchBST(root.right, val);}
        else {node = searchBST(root.left, val);}
        return node;
    }
}
```

## B

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Search in a Binary Search Tree.
    Memory Usage: 39.6 MB, less than 49.49% of Java online submissions for Search in a Binary Search Tree.
     */
    public TreeNode searchBST(TreeNode root, int val) {
        if (root == null) {return null;}

        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);

        while(!queue.isEmpty()){
            TreeNode node = queue.poll();
            if (node == null) {continue;}
            if (node.val == val) {return node;}
            if (node.val < val) {queue.offer(node.right);}
            else {queue.offer(node.left);}
        }

        return null;
    }
}
```

