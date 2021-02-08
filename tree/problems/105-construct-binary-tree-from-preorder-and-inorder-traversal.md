---
description: Medium
---

# 105 Construct Binary Tree from Preorder and Inorder Traversal

```text
//Given preorder and inorder traversal of a tree, construct the binary tree.
//
//Note:
//You may assume that duplicates do not exist in the tree.
//
//For example, given
//
//preorder = [3,9,20,15,7]
//inorder = [9,3,15,20,7]
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
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Construct Binary Tree from Preorder and Inorder Traversal.
    Memory Usage: 38.9 MB, less than 79.63% of Java online submissions for Construct Binary Tree from Preorder and Inorder Traversal.
     */
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        return helper(preorder, inorder, (long)Integer.MAX_VALUE+1);
    }
​
    int pre = 0;
    int in = 0;
    private TreeNode helper(int[] preorder, int[] inorder, long stop) {
        if (pre == preorder.length) {
            return null;
        }
        if (inorder[in] == stop) {
            in++;
            return null;
        }
        int rootVal = preorder[pre++];
        TreeNode root = new TreeNode(rootVal);
        root.left = helper(preorder, inorder, rootVal);
        root.right = helper(preorder, inorder, stop);
        return root;
    }
}
```

## **B1 \[a,b\)**

```text
//[a,b)
public class Solution {
    /*
    Runtime: 1 ms, faster than 98.26% of Java online submissions for Construct Binary Tree from Preorder and Inorder Traversal.
Memory Usage: 39.1 MB, less than 56.56% of Java online submissions for Construct Binary Tree from Preorder and Inorder Traversal.7  
     */
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < inorder.length; i++) {
            map.put(inorder[i], i);
        }
        return helper(preorder, 0, preorder.length, inorder, 0, inorder.length, map);
    }
    private TreeNode helper(int[] preorder, int pStart, int pEnd,
                            int[] inorder, int iStart, int iEnd,
                            HashMap<Integer, Integer> map) {
        if (pStart == pEnd) {return null;}
​
        int rootVal = preorder[pStart];
        TreeNode root = new TreeNode(rootVal);
        int iRootIndex = map.get(rootVal);
        int leftNum = iRootIndex - iStart;
        root.left = helper(preorder, pStart+1, pStart+leftNum+1,
                        inorder, iStart, iRootIndex, map);
        root.right = helper(preorder, pStart+leftNum+1, pEnd,
                        inorder, iRootIndex+1, iEnd, map);
        return root;
    }
}
```

## **B2 \[a,b\]**

```text
//[a,b]
public class Solution {
    /*
    Runtime: 1 ms, faster than 98.26% of Java online submissions for Construct Binary Tree from Preorder and Inorder Traversal.
    Memory Usage: 39.1 MB, less than 45.18% of Java online submissions for Construct Binary Tree from Preorder and Inorder Traversal.
     */
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        Map<Integer, Integer> inMap = new HashMap<>();
​
        for(int i = 0; i < inorder.length; i++) {
            inMap.put(inorder[i], i);
        }
​
        TreeNode root = buildTree(preorder, 0, preorder.length - 1,
                                inorder, 0, inorder.length - 1,
                                inMap);
        return root;
    }
​
    public TreeNode buildTree(int[] preorder, int preStart, int preEnd,
                              int[] inorder, int inStart, int inEnd,
                              Map<Integer, Integer> inMap) {
        if(preStart > preEnd || inStart > inEnd) {return null;}
​
        TreeNode root = new TreeNode(preorder[preStart]);
        int inRoot = inMap.get(root.val);
        int numsLeft = inRoot - inStart;
​
        root.left = buildTree(preorder, preStart + 1, preStart + numsLeft,
                            inorder, inStart, inRoot - 1, inMap);
        root.right = buildTree(preorder, preStart + numsLeft + 1, preEnd,
                            inorder, inRoot + 1, inEnd, inMap);
​
        return root;
    }
}
```

## **C**

```text
public class Solution {
    /*
    Runtime: 7 ms, faster than 9.97% of Java online submissions for Construct Binary Tree from Preorder and Inorder Traversal.
    Memory Usage: 39.3 MB, less than 24.84% of Java online submissions for Construct Binary Tree from Preorder and Inorder Traversal.
     */
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        if(preorder==null || inorder==null || inorder.length==0 || preorder.length==0) {
            return null;
        }
​
        TreeNode root = new TreeNode(preorder[0]);
        if(preorder.length==1) {
            return root;
        }
​
        int breakindex = -1;
        for(int i=0;i<inorder.length;i++) {
            if(inorder[i]==preorder[0]) {
                breakindex=i; 
                break;
            }
        }
​
        int[] subleftpre  = Arrays.copyOfRange(preorder,1,breakindex+1);
        int[] subleftin   = Arrays.copyOfRange(inorder,0,breakindex);
        int[] subrightpre = Arrays.copyOfRange(preorder,breakindex+1,preorder.length);
        int[] subrightin  = Arrays.copyOfRange(inorder,breakindex+1,inorder.length);
​
        root.left  = buildTree(subleftpre,subleftin);
        root.right = buildTree(subrightpre,subrightin);
        return root;
    }
}
```

## **D**

```text
public class Solution {
    /*
    Runtime: 1 ms, faster than 98.26% of Java online submissions for Construct Binary Tree from Preorder and Inorder Traversal.
    Memory Usage: 38.8 MB, less than 88.77% of Java online submissions for Construct Binary Tree from Preorder and Inorder Traversal.
     */
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        if (preorder.length == 0) {
            return null;
        }
        Deque<TreeNode> stack = new ArrayDeque<>();
        int pre = 0;
        int in = 0;
        TreeNode curRoot = new TreeNode(preorder[pre]);
        TreeNode root = curRoot;
        stack.push(curRoot);
        pre++;
        while (pre < preorder.length) {
            if (curRoot.val == inorder[in]) {
                while (!stack.isEmpty() && stack.peek().val == inorder[in]) {
                    curRoot = stack.pop();
                    in++;
                }
                curRoot.right = new TreeNode(preorder[pre]);
                curRoot = curRoot.right;
                stack.push(curRoot);
                pre++;
            } else {
                curRoot.left = new TreeNode(preorder[pre]);
                curRoot = curRoot.left;
                stack.push(curRoot);
                pre++;
            }
        }
        return root;
    }
}
```

