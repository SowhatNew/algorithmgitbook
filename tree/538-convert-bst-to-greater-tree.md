---
description: Medium
---

# 538 Convert BST to Greater Tree

```text
Given the root of a Binary Search Tree (BST), convert it to a Greater Tree such that 
every key of the original BST is changed to the original key plus sum of all keys greater than the original key in BST.

As a reminder, a binary search tree is a tree that satisfies these constraints:

The left subtree of a node contains only nodes with keys less than the node's key.
The right subtree of a node contains only nodes with keys greater than the node's key.
Both the left and right subtrees must also be binary search trees.

Example 1:
Input: root = [4,1,6,0,2,5,7,null,null,null,3,null,null,null,8]
Output: [30,36,21,36,35,26,15,null,null,null,33,null,null,null,8]

Example 2:
Input: root = [0,null,1]
Output: [1,null,1]

Example 3:
Input: root = [1,0,2]
Output: [3,3,2]

Example 4:
Input: root = [3,2,4,1]
Output: [7,9,4,10]
 

Constraints:
The number of nodes in the tree is in the range [0, 104].
-104 <= Node.val <= 104
All the values in the tree are unique.
root is guaranteed to be a valid binary search tree.
```

## A

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Convert BST to Greater Tree.
    Memory Usage: 39.2 MB, less than 68.74% of Java online submissions for Convert BST to Greater Tree.
     */
    public TreeNode convertBST(TreeNode root) {
        dfs(root);
        return root;
    }
    int sum = 0;
    private void dfs(TreeNode root) {
        if (root == null) {
            return ;
        }
        dfs(root.right);
        sum += root.val;
        root.val = sum;
        dfs(root.left);
    }
}
```

## B

```text
public class Solution {
    /*
    Runtime: 1 ms, faster than 43.31% of Java online submissions for Convert BST to Greater Tree.
    Memory Usage: 39.1 MB, less than 88.41% of Java online submissions for Convert BST to Greater Tree.
     */
    public TreeNode convertBST(TreeNode root) {
        if (root == null) {
            return root;
        }

        Deque<TreeNode> stack = new ArrayDeque<>();
        TreeNode cur = root;
        int sum = 0;
        while (cur != null || !stack.isEmpty()) {
            while (cur != null) {
                stack.push(cur);
                cur = cur.right;
            }
            TreeNode node = stack.pop();
            sum += node.val;
            node.val = sum;
            cur = node.left;
        }
        return root;
    }
}
```

