---
description: Easy
---

# 530 Minimum Absolute Difference in BST

```text
//Given a binary search tree with non-negative values,
// find the minimum absolute difference between values of any two nodes.
//Example:
//Input:
//   1
//    \
//     3
//    /
//   2
//Output:1
//Explanation:
//The minimum absolute difference is 1, which is the difference between 2 and 1 (or between 2 and 3).
```

## A

```text
public class Solution {

    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Minimum Absolute Difference in BST.
    Memory Usage: 38.6 MB, less than 71.56% of Java online submissions for Minimum Absolute Difference in BST.
     */
    Integer prev;
    int minDiff = Integer.MAX_VALUE;
    public int getMinimumDifference(TreeNode root) {
        inorder(root);
        return minDiff;
    }
    private void inorder(TreeNode root) {
        if (root == null) {return;}
        inorder(root.left);
        if (prev != null) {
            minDiff = Math.min(minDiff, Math.abs(root.val - prev));
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
    Runtime: 11 ms, faster than 7.49% of Java online submissions for Minimum Absolute Difference in BST.
    Memory Usage: 42.9 MB, less than 5.88% of Java online submissions for Minimum Absolute Difference in BST.
     */
    public int getMinimumDifference(TreeNode root) {
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        List<Integer> list = new ArrayList<>();

        while(!stack.isEmpty()){
            TreeNode current = stack.pop();
            list.add(current.val);
            if(current.right != null) stack.push(current.right);
            if(current.left != null) stack.push(current.left);
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

