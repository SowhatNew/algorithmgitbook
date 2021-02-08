---
description: Easy
---

# 783 Minimum Distance Between BST Nodes

```text
//Given a Binary Search Tree (BST) with the root node root, return the minimum difference
// between the values of any two different nodes in the tree.
//Note:
//The size of the BST will be between 2 and 100.
//The BST is always valid, each node's value is an integer, and each node's value is different.
//This question is the same as 530
```

## A

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Minimum Distance Between BST Nodes.
    Memory Usage: 36.5 MB, less than 79.05% of Java online submissions for Minimum Distance Between BST Nodes.
     */
    int min = Integer.MAX_VALUE;
    Integer prev;
    public int minDiffInBST(TreeNode root) {
        // The size of the BST will be between 2 and 100.
        inorder(root);
        return min;
    }
    private void inorder(TreeNode root) {
        if (root == null) {return;}
        inorder(root.left);
        if (prev != null) {
            min = Math.min(min, Math.abs(root.val - prev));
        }
        prev = root.val;
        inorder(root.right);
    }
}
```

## B

```text
public class Solution {
    /*
    Runtime: 1 ms, faster than 16.13% of Java online submissions for Minimum Distance Between BST Nodes.
    Memory Usage: 36.7 MB, less than 30.81% of Java online submissions for Minimum Distance Between BST Nodes.
     */
    public int minDiffInBST(TreeNode root) {
        Deque<TreeNode> stack = new LinkedList<>();
        stack.push(root);
        List<Integer> list = new ArrayList<>();

        while(!stack.isEmpty()){
            TreeNode current = stack.pop();
            list.add(current.val);
            if(current.right != null) {stack.push(current.right);}
            if(current.left != null) {stack.push(current.left);}
        }

        Collections.sort(list);
        int minDiff = Integer.MAX_VALUE;
        for(int i = 0 ; i <list.size()-1; i++){
            if(list.get(i+1) - list.get(i) < minDiff){
                minDiff = list.get(i+1) - list.get(i);
            }
        }
        return minDiff;
    }
}
```

