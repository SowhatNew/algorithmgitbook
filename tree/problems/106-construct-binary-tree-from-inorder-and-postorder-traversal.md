---
description: Medium
---

# 106 Construct Binary Tree from Inorder and Postorder Traversal

```text
//Given inorder and postorder traversal of a tree, construct the binary tree.
//
//Note:
//You may assume that duplicates do not exist in the tree.
//
//For example, given
//
//inorder = [9,3,15,20,7]
//postorder = [9,15,7,20,3]
//Return the following binary tree:
//
//    3
//   / \
//  9  20
//    /  \
//   15   7
```

## **A**

```text
public class Solution {
    /*
    Runtime: 1 ms, faster than 96.04% of Java online submissions for Construct Binary Tree from Inorder and Postorder Traversal.
    Memory Usage: 39.2 MB, less than 35.93% of Java online submissions for Construct Binary Tree from Inorder and Postorder Traversal.
     */
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < inorder.length; i++) {
            map.put(inorder[i], i);
        }
        return helper(postorder, 0, postorder.length,
                inorder, 0, inorder.length, map);
    }
​
    private TreeNode helper(int[] postorder, int pStart, int pEnd,
                            int[] inorder, int iStart, int iEnd,
                            HashMap<Integer, Integer> map) {
        if (pStart == pEnd) {
            return null;
        }
        int rootVal = postorder[pEnd-1];
        TreeNode root = new TreeNode(rootVal);
        int iRootIndex = map.get(rootVal);
        int leftNum = iRootIndex - iStart;
        root.left = helper(postorder, pStart, pStart + leftNum,
                inorder, iStart, iRootIndex, map);
        root.right = helper(postorder, pStart + leftNum, pEnd - 1,
                inorder, iRootIndex + 1, iEnd, map);
        return root;
    }
}
```

## **B**

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Construct Binary Tree from Inorder and Postorder Traversal.
    Memory Usage: 38.9 MB, less than 80.73% of Java online submissions for Construct Binary Tree from Inorder and Postorder Traversal.
     */
    int post;
    int in;
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        post = postorder.length - 1;
        in = inorder.length - 1;
        return helper(inorder, postorder, (long)Integer.MIN_VALUE-1);
    }
    private TreeNode helper(int[] inorder, int[] postorder, long stop) {
        if (post == -1) {return null;}
        if (inorder[in] == stop) {
            in--;
            return null;
        }
        int rootVal = postorder[post--];
        TreeNode root = new TreeNode(rootVal);
        root.right = helper(inorder, postorder, rootVal);
        root.left = helper(inorder, postorder, stop);
        return root;
    }
}
```

## **C**

```text
public class Solution {
    /*
    Runtime: 1 ms, faster than 96.04% of Java online submissions for Construct Binary Tree from Inorder and Postorder Traversal.
    Memory Usage: 38.4 MB, less than 99.33% of Java online submissions for Construct Binary Tree from Inorder and Postorder Traversal.
     */
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        if (postorder.length == 0) {
            return null;
        }
        Deque<TreeNode> stack = new ArrayDeque<>();
        int post = postorder.length - 1;
        int in = inorder.length - 1;
        TreeNode curRoot = new TreeNode(postorder[post]);
        TreeNode root = curRoot;
        stack.push(curRoot);
        post--;
        while (post >=  0) {
            if (curRoot.val == inorder[in]) {
                while (!stack.isEmpty() && stack.peek().val == inorder[in]) {
                    curRoot = stack.peek();
                    stack.pop();
                    in--;
                }
                curRoot.left = new TreeNode(postorder[post]);
                curRoot = curRoot.left;
                stack.push(curRoot);
                post--;
            } else {
                curRoot.right = new TreeNode(postorder[post]);
                curRoot = curRoot.right;
                stack.push(curRoot);
                post--;
            }
        }
        return root;
    }
}
```

