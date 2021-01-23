---
description: Easy
---

# 617 Merge Two Binary Trees

```text
//Given two binary trees and imagine that when you put one of them to cover the other,
// some nodes of the two trees are overlapped while the others are not.
//You need to merge them into a new binary tree. The merge rule is that if two nodes overlap,
// then sum node values up as the new value of the merged node.
// Otherwise, the NOT null node will be used as the node of new tree.
//Input:
//	Tree 1                     Tree 2
//          1                         2
//         / \                       / \
//        3   2                     1   3
//       /                           \   \
//      5                             4   7
//Output:
//Merged tree:
//	     3
//	    / \
//	   4   5
//	  / \   \
//	 5   4   7
//Note: The merging process must start from the root nodes of both trees.
```

## A1

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Merge Two Binary Trees.
    Memory Usage: 39.3 MB, less than 57.38% of Java online submissions for Merge Two Binary Trees.
     */
    public TreeNode mergeTrees(TreeNode t1, TreeNode t2) {
        if (t1 == null && t2 == null) {return null;}
        if (t1 == null) {return t2;}
        if (t2 == null) {return t1;}

        TreeNode newNode = new TreeNode(t1.val + t2.val);

        newNode.left = mergeTrees(t1.left, t2.left);
        newNode.right = mergeTrees(t1.right, t2.right);

        return newNode;
    }
}
```

A2

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Merge Two Binary Trees.
    Memory Usage: 39 MB, less than 82.12% of Java online submissions for Merge Two Binary Trees.
     */
    public TreeNode mergeTrees(TreeNode t1, TreeNode t2) {
        if (t1 == null) {return t2;}
        if (t2 == null) {return t1;}
        return new TreeNode(t1.val + t2.val,
                mergeTrees(t1.left, t2.left),
                mergeTrees(t1.right, t2.right));
    }
}
```

## B

```text
public class Solution {
    /*
    Runtime: 1 ms, faster than 28.68% of Java online submissions for Merge Two Binary Trees.
    Memory Usage: 38.7 MB, less than 99.77% of Java online submissions for Merge Two Binary Trees.
     */
    public TreeNode mergeTrees(TreeNode t1, TreeNode t2) {
        if (t1 == null) {return t2;}
        if (t2 == null) {return t1;}

        Deque<TreeNode> stack = new LinkedList<>();
        stack.push(t1);
        stack.push(t2);

        while (!stack.isEmpty()) {
            TreeNode second = stack.pop();
            TreeNode first = stack.pop();

            if (first != null && second != null) {
                first.val += second.val;
                if (first.left == null) {
                    first.left = second.left;
                } else {
                    stack.push(first.left);
                    stack.push(second.left);
                }

                if (first.right == null){
                    first.right = second.right;
                } else {
                    stack.push(first.right);
                    stack.push(second.right);
                }
            }
        }
        return t1;
    }
}
```

