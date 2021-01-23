---
description: Easy
---

# 671 Second Minimum Node In a Binary Tree

```text
//Given a non-empty special binary tree consisting of nodes with the non-negative value,
// where each node in this tree has exactly two or zero sub-node.
// If the node has two sub-nodes, then this node's value is the smaller value among its two sub-nodes.
// More formally, the property root.val = min(root.left.val, root.right.val) always holds.
//Given such a binary tree, you need to output the second minimum value
// in the set made of all the nodes' value in the whole tree.
//If no such second minimum value exists, output -1 instead.
//Constraints:
//The number of nodes in the tree is in the range [1, 25].
//1 <= Node.val <= 231 - 1
//root.val == min(root.left.val, root.right.val) for each internal node of the tree.
```

## A

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Second Minimum Node In a Binary Tree.
    Memory Usage: 36.3 MB, less than 45.03% of Java online submissions for Second Minimum Node In a Binary Tree.
     */
    long target = Long.MAX_VALUE;
    public int findSecondMinimumValue(TreeNode root) {
        if (root == null) {return -1;}
        helper(root);
        return (target <= Integer.MAX_VALUE) ? (int)target : -1;
    }
    private void helper(TreeNode root) {
        if (root == null) {return;}

        if (root.left != null && root.left.val != root.val) {
            target = Math.min(target, root.left.val);
        }
        if (root.right != null && root.right.val != root.val) {
            target = Math.min(target, root.right.val);
        }

        helper(root.left);
        helper(root.right);
    }
}

```

## B

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Second Minimum Node In a Binary Tree.
    Memory Usage: 36.4 MB, less than 30.16% of Java online submissions for Second Minimum Node In a Binary Tree.
     */    
    Set<Integer> set = new HashSet<>();

    public void helper(TreeNode root) {
        if (root == null) {return;}
        set.add(root.val);
        helper(root.left);
        helper(root.right);
    }
    public int findSecondMinimumValue(TreeNode root) {
        helper(root);
        int min = root.val;
        long target = Long.MAX_VALUE;
        for (int i : set) {
            if (i > min && i < target) {
                target = i;
            }
        }
        return (target < Long.MAX_VALUE) ? (int)target : -1;
    }
}
```

