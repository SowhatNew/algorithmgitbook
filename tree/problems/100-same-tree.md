---
description: Easy
---

# 100 Same Tree

```text
Given the roots of two binary trees p and q, write a function to check if they are the same or not.
Two binary trees are considered the same if they are structurally identical, and the nodes have the same value.
```

## A

```text
public class Solution {
	/*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Same Tree.
    Memory Usage: 36.5 MB, less than 46.80% of Java online submissions for Same Tree.
     */
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if(p == null && q == null) {return true;}
        if(p == null && q != null) {return false;}
        if(p != null && q == null) {return false;}
        if(p.val != q.val) {return false;}
        return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
    }
  }
```

## B

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Same Tree.
    Memory Usage: 36.2 MB, less than 80.22% of Java online submissions for Same Tree.
     */
    public boolean isSameTree2(TreeNode p, TreeNode q) {
        Queue<Pair<TreeNode, TreeNode>> queue =
                new LinkedList<Pair<TreeNode, TreeNode>>();
        queue.add(new Pair<>(p, q));
        while (queue.peek() != null) {
            Pair<TreeNode, TreeNode> temp = queue.remove();
            TreeNode ptemp = temp.first;
            TreeNode qtemp = temp.second;
            if(ptemp == null && qtemp == null) continue;
            if(ptemp == null && qtemp != null) return false;
            if(ptemp != null && qtemp == null) return false;
            if(ptemp.val != qtemp.val) return false;
            queue.add(new Pair<>(ptemp.left, qtemp.left));
            queue.add(new Pair<>(ptemp.right, qtemp.right));
        }
        return true;
    }
}
```

