---
description: Medium
---

# 114 Flatten Binary Tree to Linked List

```text
//Given the root of a binary tree, flatten it to a linked list in-place.
//Input: root = [1,2,5,3,4,null,6]
//Output: [1,null,2,null,3,null,4,null,5,null,6]   
```

## **A**

```text
public class Solution {
    /*
    Runtime: 1 ms, faster than 28.69% of Java online submissions for Flatten Binary Tree to Linked List.
    Memory Usage: 38.2 MB, less than 83.33% of Java online submissions for Flatten Binary Tree to Linked List.
     */
    public void flatten(TreeNode root) {
        Deque<TreeNode> stack = new ArrayDeque<>();
        while (root != null) {
            if (root.left != null) {
                if (root.right != null) {
                    stack.push(root.right);
                }
                root.right = root.left;
                root.left = null;
            }
            root = root.right;
            while (root != null && root.left == null && root.right == null && !stack.isEmpty()) {
                root.right = stack.pop();
                root = root.right;
            }
        }
    }
}
```

## **B**

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Flatten Binary Tree to Linked List.
    Memory Usage: 38.6 MB, less than 45.23% of Java online submissions for Flatten Binary Tree to Linked List.
     */
    public void flatten(TreeNode root) {
        while (root != null) {
            if (root.left != null) {
                TreeNode pre = root.left;
                while (pre.right != null) {
                    pre = pre.right;
                }
                pre.right = root.right;
                root.right = root.left;
                root.left = null;
            }
            root = root.right;
        }
    }
}
```

## **C**

```text
public class Solution {
    /*
    Runtime: 1 ms, faster than 28.69% of Java online submissions for Flatten Binary Tree to Linked List.
    Memory Usage: 38.3 MB, less than 71.61% of Java online submissions for Flatten Binary Tree to Linked List.
     */
    public void flatten(TreeNode root) {
        Deque<TreeNode> stack = new ArrayDeque<>();
        TreeNode cur = root;
        TreeNode pre = null;
        while (cur != null || !stack.isEmpty()) {
            while (cur != null) {
                stack.push(cur);
                cur = cur.right;
            }
            cur = stack.peek();
            if (cur.left == null || cur.left == pre) {
                stack.pop();
                cur.right = pre;
                cur.left = null;
                pre = cur;
                cur = null;
            } else {
                cur = cur.left;
            }
        }
    }
}
```

## **D**

```text
public class Solution {
    /*
    Runtime: 1 ms, faster than 28.69% of Java online submissions for Flatten Binary Tree to Linked List.
    Memory Usage: 38.6 MB, less than 45.23% of Java online submissions for Flatten Binary Tree to Linked List.
     */
    public void flatten(TreeNode root) {
        if (root == null) {return;}
        Deque<TreeNode> stack = new ArrayDeque<>();
        stack.push(root);
        TreeNode pre = null;
        while (!stack.isEmpty()) {
            TreeNode temp = stack.pop();
            if (pre != null) {
                pre.right = temp;
                pre.left = null;
            }
            if (temp.right != null) {
                stack.push(temp.right);
            }
            if (temp.left != null) {
                stack.push(temp.left);
            }
            pre = temp;
        }
    }
}
```

### 

