---
description: Medium
---

# 701 Insert into a Binary Search Tree

```text
You are given the root node of a binary search tree (BST) and a value to insert into the tree. 
Return the root node of the BST after the insertion. 
It is guaranteed that the new value does not exist in the original BST.

Notice that there may exist multiple valid ways for the insertion, 
as long as the tree remains a BST after insertion. 
You can return any of them.

Example 1:
Input: root = [4,2,7,1,3], val = 5
​
Output: [4,2,7,1,3,5]

Example 2:​
Input: root = [40,20,60,10,30,50,70], val = 25
Output: [40,20,60,10,30,50,70,null,null,25]
​

Example 3:​
Input: root = [4,2,7,1,3,null,null,null,null,null,null], val = 5
Output: [4,2,7,1,3,5]
 

Constraints:

The number of nodes in the tree will be in the range [0, 104].
-108 <= Node.val <= 108
All the values Node.val are unique.
-108 <= val <= 108
It's guaranteed that val does not exist in the original BST.
```

## A

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Insert into a Binary Search Tree.
    Memory Usage: 51.2 MB, less than 14.97% of Java online submissions for Insert into a Binary Search Tree.
     */
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if (root == null) {
            root = new TreeNode(val);
        } else if (root.val < val) {
            root.right = insertIntoBST(root.right, val);
        } else if (root.val > val) {
            root.left = insertIntoBST(root.left, val);
        }
        return root;
    }
}
```

## B1

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Insert into a Binary Search Tree.
    Memory Usage: 51.6 MB, less than 6.46% of Java online submissions for Insert into a Binary Search Tree.
     */
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if (root == null) {
            return new TreeNode(val);
        }

        TreeNode cur = root;
        TreeNode pre = root;
        boolean isLeft = false;
        while (cur != null) {
            if (cur.val < val) {
                isLeft = false;
                pre = cur;
                cur = cur.right;
            } else if (cur.val > val) {
                isLeft = true;
                pre = cur;
                cur = cur.left;
            }
        }

        if (isLeft) {
            pre.left = new TreeNode(val);
        } else {
            pre.right = new TreeNode(val);
        }

        return root;
    }
}
```

## B2

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Insert into a Binary Search Tree.
    Memory Usage: 51.4 MB, less than 8.76% of Java online submissions for Insert into a Binary Search Tree.
     */
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if (root == null) {
            return new TreeNode(val);
        }

        TreeNode pre = root;
        TreeNode cur = root;
        boolean isLeft = false;
        while (pre != null) {
            if (cur == null) {
                cur = new TreeNode(val);
            } else if (cur.val == val) {
                if (isLeft) {
                    pre.left = cur;
                } else {
                    pre.right = cur;
                }
                break;
            } else if (cur.val < val) {
                pre = cur;
                isLeft = false;
                cur = cur.right;
            } else if (cur.val > val) {
                pre = cur;
                isLeft = true;
                cur = cur.left;
            }
        }

        return root;
    }
}
```

