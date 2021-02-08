---
description: Easy
---

# 938 Range Sum of BST

```text
// Given the root node of a binary search tree, 
//return the sum of values of all nodes with a value in the range [low, high].
```

## A

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Range Sum of BST.
    Memory Usage: 46.7 MB, less than 94.63% of Java online submissions for Range Sum of BST.     */
    int low, high;
    int sum = 0;
    public int rangeSumBST(TreeNode root, int low, int high) {
        this.low = low;
        this.high = high;
        dfs(root);
        return sum;
    }
    public void dfs(TreeNode root) {
        if (root == null) {return;}
        if (root.val >= low && root.val <= high) {
            sum += root.val;
        }
        if (root.val < low){
            dfs(root.right);
        } else if(root.val > high){
            dfs(root.left);
        } else {
            dfs(root.left);
            dfs(root.right);
        }
    }
}
```

## B

```text
public class Solution {
    /*
    Runtime: 2 ms, faster than 14.61% of Java online submissions for Range Sum of BST.
    Memory Usage: 43.7 MB, less than 99.98% of Java online submissions for Range Sum of BST.     */
    int sum = 0;
    public int rangeSumBST(TreeNode root, int low, int high) {
        bfs(root, low, high);
        return sum;
    }
    public void bfs(TreeNode root, int low, int high) {
        if (root == null) {return;}

        Deque<TreeNode> stack = new LinkedList<>();
        stack.push(root);

        while(!stack.isEmpty()){
            TreeNode node = stack.pop();
            if (node == null) {continue;}
            if (node.val >= low && node.val <= high) {
                sum += node.val;
                stack.push(node.right);
                stack.push(node.left);
            }
            if (node.val < low){
                stack.push(node.right);
            } else if(node.val > high){
                stack.push(node.left);
            }
        }
    }
}
```

