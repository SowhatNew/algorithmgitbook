---
description: Medium
---

# 450 Delete Node in a BST

```text
Given a root node reference of a BST and a key, 
delete the node with the given key in the BST. 
Return the root node reference (possibly updated) of the BST.

Basically, the deletion can be divided into two stages:

Search for a node to remove.
If the node is found, delete the node.
Follow up: Can you solve it with time complexity O(height of tree)?

Example 1:
Input: root = [5,3,6,2,4,null,7], key = 3
Output: [5,4,6,2,null,null,7]
Explanation: Given key to delete is 3. So we find the node with value 3 and delete it.
One valid answer is [5,4,6,2,null,null,7], shown in the above BST.
Please notice that another valid answer is [5,2,6,null,4,null,7] and it's also accepted.

Example 2:
Input: root = [5,3,6,2,4,null,7], key = 0
Output: [5,3,6,2,4,null,7]
Explanation: The tree does not contain a node with value = 0.

Example 3:
Input: root = [], key = 0
Output: []

Constraints:
The number of nodes in the tree is in the range [0, 104].
-105 <= Node.val <= 105
Each node has a unique value.
root is a valid binary search tree.
-105 <= key <= 105
```

## A1

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Delete Node in a BST.
    Memory Usage: 39.4 MB, less than 63.18% of Java online submissions for Delete Node in a BST.
     */
    public TreeNode deleteNode(TreeNode root, int key) {
        if (root == null) {
            return null;
        }
        if (root.val < key) {
            root.right = deleteNode(root.right, key);
        } else if (root.val > key) {
            root.left = deleteNode(root.left, key);
        } else {
//            if (root.left == null && root.right == null) {
//                return null;
//            }
            if (root.left == null) {
                return root.right;
            }
            if (root.right == null) {
                return root.left;
            }

            TreeNode cur = root.right;
            while (cur.left != null) {
                cur = cur.left;
            }
            cur.left = root.left;
            return root.right;
        }
        return root;
    }
}
```

## A2

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Delete Node in a BST.
    Memory Usage: 46.7 MB, less than 11.34% of Java online submissions for Delete Node in a BST.
     */
    public TreeNode deleteNode(TreeNode root, int key) {
        if (root == null) {
            return null;
        }
        if (root.val < key) {
            root.right = deleteNode(root.right, key);
        } else if (root.val > key) {
            root.left = deleteNode(root.left, key);
        } else {
//            if (root.left == null && root.right == null) {
//                return null;
//            }
            if (root.left == null) {
                return root.right;
            }
            if (root.right == null) {
                return root.left;
            }

            TreeNode cur = root.right;
            while (cur.left != null) {
                cur = cur.left;
            }
            TreeNode temp = cur;
            root = deleteNode(root, cur.val);
            temp.left = root.left;
            temp.right = root.right;
            return temp;
        }
        return root;
    }
}
```

## B

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Delete Node in a BST.
    Memory Usage: 47 MB, less than 5.55% of Java online submissions for Delete Node in a BST.
     */
    public TreeNode deleteNode(TreeNode root, int key) {
        if (root == null) {
            return root;
        }

        TreeNode cur = root;
        TreeNode pre = null;
        boolean isLeft = false;
        while (true) {
            if (cur == null) {
                return root;
            }
            if (cur.val == key) {
                break;
            }
            if (cur.val < key) {
                isLeft = false;
                pre = cur;
                cur = cur.right;
            } else if (cur.val > key) {
                isLeft = true;
                pre = cur;
                cur = cur.left;
            }
        }

        TreeNode temp;
        if (cur.left == null) {
            temp = cur.right;
        } else if (cur.right == null) {
            temp = cur.left;
        } else {
            TreeNode node = cur.right;
            while (node.left != null) {
                node = node.left;
            }
            node.left = cur.left;
            temp = cur.right;
        }

        if (pre != null) {
            if (isLeft) {
                pre.left = temp;
            } else {
                pre.right = temp;
            }
        } else {
            return temp;
        }

        return root;
    }
}
```

