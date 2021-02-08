---
description: Easy
---

# 108 Convert Sorted Array to Binary Search Tree

```text
// Given an array where elements are sorted in ascending order, convert it to a height balanced BST.
// For this problem, a height-balanced binary tree is defined as a binary tree in which 
// the depth of the two subtrees of every node never differ by more than 1.
// Example:
// Given the sorted array: [-10,-3,0,5,9],
// One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:
//       0
//      / \
//    -3   9
//    /   /
//  -10  5
```

```text
class Solution {
    /**
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Convert Sorted Array to Binary Search Tree.
    Memory Usage: 38.7 MB, less than 66.69% of Java online submissions for Convert Sorted Array to Binary Search Tree.
     */    
    public TreeNode sortedArrayToBST(int[] nums) {
        return subTree(nums, 0, nums.length);
    }

    private TreeNode subTree(int[] nums, int low, int high) {
        TreeNode root = null;
        if (low < high) {
            int mid = low + (high - low) / 2;
            root = new TreeNode(nums[mid]);
            root.left = subTree(nums, low, mid);
            root.right = subTree(nums, mid+1, high);
        }
        return root;
    }
}
```

