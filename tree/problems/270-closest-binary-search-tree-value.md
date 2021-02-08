---
description: Easy
---

# 270 Closest Binary Search Tree Value

```text
//Given a non-empty binary search tree and a target value, find the value in the BST that is closest to the target.
//Note:
//Given target value is a floating point.
//You are guaranteed to have only one unique value in the BST that is closest to the target.
//Input: root = [4,2,5,1,3], target = 3.714286
//
//    4
//   / \
//  2   5
// / \
//1   3
//
//Output: 4
```

## A

```text
public class Solution {
    int goal;
    double min = Double.MAX_VALUE;

    public int closestValue(TreeNode root, double target) {
        helper(root, target);
        return goal;
    }
    public void helper(TreeNode root, double target) {
        if (root == null) {return;}
        if (Math.abs(root.val - target) < min) {
            min = Math.abs(root.val - target);
            goal = root.val;
        }
        if (target < root.val) {helper(root.left, target);}
        else {helper(root.right, target);}
    }
}
```

## B

```text
class Solution {
    public int closestValue(TreeNode root, double target) {
        double min = Double.MAX_VALUE;
        int result = root.val;

        while (root != null) {
            if (Math.abs(root.val - target) < min) {
                min = Math.abs(root.val - target);
                result = root.val;
            }
            if (target > root.val) {root = root.right;}
            else if (target < root.val){root = root.left;}
            else {return root.val;}
        }
        return result;
    }
}
```

