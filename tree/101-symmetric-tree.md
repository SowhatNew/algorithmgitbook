---
description: Easy
---

# 101 Symmetric Tree

```text
Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).
For example, this binary tree [1,2,2,3,4,4,3] is symmetric:
    1
   / \
  2   2
 / \ / \
3  4 4  3
But the following [1,2,2,null,3,null,3] is not:
    1
   / \
  2   2
   \   \
   3    3
```

## A

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Symmetric Tree.
    Memory Usage: 37.3 MB, less than 32.08% of Java online submissions for Symmetric Tree.
     */
    public boolean isSymmetric(TreeNode root) {
        if(root == null) return true;
        return helper(root.left, root.right);
    }
    private boolean helper(TreeNode leftHalf, TreeNode rightHalf){
        if(leftHalf == null && rightHalf == null) return true;
        if(leftHalf == null && rightHalf != null) return false;
        if(leftHalf != null && rightHalf == null) return false;
        if(leftHalf.val != rightHalf.val) return false;

        return helper(leftHalf.left, rightHalf.right)
            && helper(leftHalf.right, rightHalf.left);
    }
}
```

## B

```text
public class Solution {
	/*
	Runtime: 1 ms, faster than 24.44% of Java online submissions for Symmetric Tree.
	Memory Usage: 38.4 MB, less than 15.89% of Java online submissions for Symmetric Tree.
     */
    // 空节点没有孩子, 空节点应当作为孩子
    public boolean isSymmetric(TreeNode root) {
        if(root == null) return true;

        Queue<TreeNode> queueLeft = new LinkedList<>(); // 1, 2, 3
        Queue<TreeNode> queueRight = new LinkedList<>(); // 6, 5, 4
        queueLeft.offer(root.left);
        queueRight.offer(root.right);

        while (queueLeft.size() > 0 && queueRight.size() > 0) {
            TreeNode leftNode = queueLeft.poll();
            TreeNode rightNode = queueRight.poll();
            
            if(leftNode == null && rightNode == null) continue;
            if(leftNode == null && rightNode != null) return false;
            if(leftNode != null && rightNode == null) return false;
            if(leftNode.val != rightNode.val) return false;
            
            queueLeft.offer(leftNode.left);
            queueLeft.offer(leftNode.right);            
            queueRight.offer(rightNode.right);
            queueRight.offer(rightNode.left);
            
        }
        if(queueLeft.size() == 0 && queueRight.size() == 0) return true;
        return false;
    }
}
```

## C

```text
public class Solution {
    /*
    Runtime: 1 ms, faster than 24.44% of Java online submissions for Symmetric Tree.
    Memory Usage: 38.3 MB, less than 22.24% of Java online submissions for Symmetric Tree.
     */
    public boolean isSymmetric(TreeNode root) {
        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);
        q.add(root);
        while (!q.isEmpty()) {
            TreeNode t1 = q.poll();
            TreeNode t2 = q.poll();
            if (t1 == null && t2 == null) continue;
            if (t1 == null || t2 == null) return false;
            if (t1.val != t2.val) return false;
            q.add(t1.left);
            q.add(t2.right);
            q.add(t1.right);
            q.add(t2.left);
        }
        return true;
    }
}
```

