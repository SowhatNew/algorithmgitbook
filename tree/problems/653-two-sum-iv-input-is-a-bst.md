---
description: Easy
---

# 653 Two Sum IV - Input is a BST

```text
// Given the root of a Binary Search Tree and a target number k, 
// return true if there exist two elements in the BST such that their sum is equal to the given target.
// [5,3,6,2,4,null,7] [8] true
// [5,3,6,2,4,null,7] [6] true
// [1] [2] false
// [0,-1,2,-3,null,null,4] [-4] true
```

## A

```text
public class Solution {
    /*
    Runtime: 1 ms, faster than 100.00% of Java online submissions for Two Sum IV - Input is a BST.
    Memory Usage: 40.1 MB, less than 53.54% of Java online submissions for Two Sum IV - Input is a BST.
     */
    TreeNode treeRoot;
    public boolean findTarget(TreeNode root, int k) {
        this.treeRoot = root;
        return helper(root, k);
    }
    private boolean helper(TreeNode root, int k) {
        if (root == null) {return false;}

        int diff = k - root.val;
        if (diff != root.val) {
            if (findX(this.treeRoot, diff)) {return true;}
        }
        return helper(root.left, k) || helper(root.right, k);
    }
    private boolean findX(TreeNode root, int k) {
        if (root == null) {return false;}
        if (root.val == k) {return true;}
        if (root.val < k) {return findX(root.right, k);}
        if (root.val > k) {return findX(root.left, k);}
        return false;
    }
}
// DFS中序遍历, 得到node.val的List, 依次相加判断, 双指针判断.
```

## B

```text
public class Solution {
    /*
    Runtime: 2 ms, faster than 98.14% of Java online submissions for Two Sum IV - Input is a BST.
    Memory Usage: 40.6 MB, less than 22.61% of Java online submissions for Two Sum IV - Input is a BST.
     */
    public boolean findTarget(TreeNode root, int k) {
        List<Integer> list = new ArrayList<>();
        inorder(root, list);

        int left = 0;
        int right = list.size() - 1;
        while (left <= right) {
            int target = k - list.get(left);
            if (list.get(right).equals(list.get(left))) {
                break;
            }else if (list.get(right) == target) {
                return true;
            }else {
                if (list.get(right) > target) {right--;}
                else {left++;}
            }
        }
        return false;

    }
    private void inorder(TreeNode root, List<Integer> list) {
        if (root == null) {return;}
        inorder(root.left, list);
        list.add(root.val);
        inorder(root.right, list);
    }
}
// BFS遍历, 得到node.val的List, 排序, 双指针查找.
```

