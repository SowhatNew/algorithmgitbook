---
description: Medium
---

# 103 Binary Tree Zigzag Level Order Traversal

```text
// 100.00% 87.66% ArrayList + zigzagHelp(TreeNode root, int level, List<List<Integer>> list) 
// 100.00% 78.04% ArrayList + zigzagHelp(TreeNode root, int level)
// 73.84% 35.80% LinkedList + zigzagHelp(TreeNode root, int level)
​
// Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).
//Given binary tree [3,9,20,null,null,15,7],
//    3
//   / \
//  9  20
//    /  \
//   15   7
//return its zigzag level order traversal as:
//[
//  [3],
//  [20,9],
//  [15,7]
//]

```

## A

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Binary Tree Zigzag Level Order Traversal.
    Memory Usage: 38.9 MB, less than 87.66% of Java online submissions for Binary Tree Zigzag Level Order Traversal.
     */
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
​
        List<List<Integer>> res = new ArrayList<>();
        zigzagHelp(root, 0, res);
        return res;
​
    }
​
    public void zigzagHelp(TreeNode root, int level, List<List<Integer>> list) {
        if (root == null) {return;}
​
        if (list.size() <= level) {
            list.add(new ArrayList<>());
        }
        if (level % 2 == 0) {
            list.get(level).add(root.val);
        }
        else {
            list.get(level).add(0, root.val);
        }
        zigzagHelp(root.left, level + 1, list);
        zigzagHelp(root.right, level + 1, list);
​
    }
}
​
```

## B

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Binary Tree Zigzag Level Order Traversal.
    Memory Usage: 39 MB, less than 78.04% of Java online submissions for Binary Tree Zigzag Level Order Traversal.
     */
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        zigzagHelp(root, 0);
        return list;
​
    }
    List<List<Integer>> list = new ArrayList<>();
    public void zigzagHelp(TreeNode root, int level) {
        if (root == null) {return;}
​
        if (list.size() <= level) {
            list.add(new ArrayList<>());
        }
        if (level % 2 == 0) {
            list.get(level).add(root.val);
        }
        else {
            list.get(level).add(0, root.val);
        }
​
        zigzagHelp(root.left, level + 1);
        zigzagHelp(root.right, level + 1);
    }
}
```

## C​

```text
public class Solution {
    /*
    Runtime: 1 ms, faster than 73.84% of Java online submissions for Binary Tree Zigzag Level Order Traversal.
    Memory Usage: 39.2 MB, less than 35.80% of Java online submissions for Binary Tree Zigzag Level Order Traversal.
     */
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        
        dfs(root, 0);
        List<List<Integer>> lists = new LinkedList<>();
        for (Deque<Integer> deque : result) {
            lists.add((LinkedList<Integer>)deque);
        }
        return lists;
    }
    List<Deque<Integer>> result = new LinkedList<>();
    private void dfs(TreeNode root, int depth) {
        if (root == null) {return;}
        if (result.size() == depth) {
            result.add(new LinkedList<>());
        }
        if ((depth & 1) == 0) {
            result.get(depth).addLast(root.val);
        } else {
            result.get(depth).addFirst(root.val);
        }
        dfs(root.left, depth+1);
        dfs(root.right, depth+1);
    }
}
```





