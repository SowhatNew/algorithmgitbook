---
description: Medium
---

# 199 Binary Tree Right Side View

```text
//Given a binary tree, imagine yourself standing on the right side of it, 
// return the values of the nodes you can see ordered from top to bottom.
//
//Example:
//
//Input: [1,2,3,null,5,null,4]
//Output: [1, 3, 4]
//Explanation:
//
//   1            <---
// /   \
//2     3         <---
// \     \
//  5     4       <---
```

## A

```text
public class Solution {
    /*
    Runtime: 1 ms, faster than 75.84% of Java online submissions for Binary Tree Right Side View.
    Memory Usage: 37.5 MB, less than 74.72% of Java online submissions for Binary Tree Right Side View.
     */
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if (root == null) {return res;}

        Deque<TreeNode> deque = new LinkedList<>();
        deque.offer(root);
        TreeNode node;
        while (!deque.isEmpty()) {
            res.add(deque.peekLast().val);
            int size = deque.size();
            for (int i = 0; i < size; i++) {
                node = deque.poll();
                if (node.left != null) {
                    deque.offer(node.left);
                }
                if (node.right != null) {
                    deque.offer(node.right);
                }
            }
        }
        return res;
    }
}
```

## B

```text
public class Solution {
    /*
    Runtime: 1 ms, faster than 75.84% of Java online submissions for Binary Tree Right Side View.
    Memory Usage: 37.5 MB, less than 74.72% of Java online submissions for Binary Tree Right Side View.
     */
    public List<Integer> rightSideView(TreeNode root) {
        res = new LinkedList<>();
        dfs(root, 0);
        return res;
    }
    List<Integer> res;
    private void dfs(TreeNode root, int level) {
        if (root == null) {return;}
        if (level == res.size()) {
            res.add(root.val);
        }
        dfs(root.right, level+1);
        dfs(root.left, level+1);
    }
}
```

