---
description: Easy
---

# 112 Path Sum

```text
// Given a binary tree and a sum, determine if the tree has a root-to-leaf path 
// such that adding up all the values along the path equals the given sum.
// Note: A leaf is a node with no children.    
```

## A

```text
class Solution{
    /*
     * Runtime: 0 ms, faster than 100.00% of Java online submissions for Path Sum.
     * Memory Usage: 39 MB, less than 54.65% of Java online submissions for Path Sum.
     */
    public boolean hasPathSum(TreeNode root, int sum) {
        if (root == null) {return false;}
        if (root.left == null && root.right == null && root.val == sum) {return true;}
        return hasPathSum(root.left, sum - root.val) || hasPathSum(root.right, sum - root.val);
    }
}
```

## B

```text
class Solution{
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Path Sum.
    Memory Usage: 38.6 MB, less than 97.38% of Java online submissions for Path Sum.
     */
    public boolean hasPathSum(TreeNode root, int sum) {
        return dfs(root, sum, 0);
    }
    private boolean dfs(TreeNode root, int sum, int pathSum) {
        if (root == null) {return false;}
        pathSum += root.val;
        if (root.left == null && root.right == null && sum == pathSum) {return true;}
        return dfs(root.left, sum, pathSum) ||
                dfs(root.right, sum, pathSum);
    }
}
```

## C

```text
class Solution{
    /*
    Runtime: 1 ms, faster than 14.41% of Java online submissions for Path Sum.
    Memory Usage: 38.5 MB, less than 97.38% of Java online submissions for Path Sum.
     */
    public boolean hasPathSum(TreeNode root, int sum) {
        if (root == null) {return false;}

        Deque<TreeNode> path = new LinkedList<>();
        Deque<Integer> sub = new LinkedList<>();
        path.push(root);
        sub.push(root.val);
        while (!path.isEmpty()) {
            TreeNode temp = path.pop();
            int tempVal = sub.pop();
            if (temp.left == null && temp.right == null && tempVal == sum) {return true;}
            if (temp.left != null) {
                path.push(temp.left);
                sub.push(temp.left.val + tempVal);
            }
            if (temp.right != null) {
                path.push(temp.right);
                sub.push(temp.right.val + tempVal);
            }
        }
        return false;
    }
}
```

