---
description: Medium
---

# 113 Path Sum II

```text
//Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.
//Note: A leaf is a node with no children.
```

## **A**

```text
public class Solution {
    /*
    Runtime: 1 ms, faster than 100.00% of Java online submissions for Path Sum II.
    Memory Usage: 39.8 MB, less than 34.44% of Java online submissions for Path Sum II.
     */
    List<List<Integer>> ll;
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        ll = new ArrayList<>();
        if (root == null) {return ll;}
        dfs(root, sum, new ArrayList<Integer>());
        return ll;
    }
    private void dfs(TreeNode root, int sum, List<Integer> list) {
        if (root == null) {return;}
        list.add(root.val);
        if (root.left == null && root.right == null && root.val == sum) {
            List<Integer> l = new ArrayList<>(list);
            ll.add(l);
        }
        sum -= root.val;
        dfs(root.left, sum, list);
        dfs(root.right, sum, list);
        list.remove(list.size()-1);
    }
}
```

## **B**

```text
public class Solution {
    /*
    Runtime: 1 ms, faster than 100.00% of Java online submissions for Path Sum II.
    Memory Usage: 39.1 MB, less than 95.14% of Java online submissions for Path Sum II.
     */
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        List<List<Integer>> res = new ArrayList<>();
        if (root == null) {return res;}
​
        Deque<TreeNode> stack = new ArrayDeque<>();
        List<Integer> temp = new ArrayList<>();
        TreeNode cur = root;
        TreeNode pre = null;
        int curSum = 0;
        while (cur != null || !stack.isEmpty()) {
            while (cur != null) {
                stack.push(cur);
                curSum += cur.val;
                temp.add(cur.val);
                cur = cur.left;
            }
            cur = stack.peek();
            if (curSum == sum && cur.left == null && cur.right == null) {
                res.add(new ArrayList<>(temp));
            }
            if (cur.right == null || cur.right == pre) {
                TreeNode node = stack.pop();
                temp.remove(temp.size()-1);
                curSum -= node.val;
                pre = cur;
                cur = null;
            } else {
                cur = cur.right;
            }
        }
        return res;
    }
}
```

