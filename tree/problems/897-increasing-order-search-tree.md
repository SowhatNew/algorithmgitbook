---
description: Easy
---

# 897 Increasing Order Search Tree

```text
//Given the root of a binary search tree, rearrange the tree in in-order
// so that the leftmost node in the tree is now the root of the tree,
// and every node has no left child and only one right child.
//Input: root = [5,3,6,2,4,null,8,1,null,null,null,7,9]
//Output: [1,null,2,null,3,null,4,null,5,null,6,null,7,null,8,null,9]
```

## A

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Increasing Order Search Tree.
    Memory Usage: 36.5 MB, less than 50.83% of Java online submissions for Increasing Order Search Tree.
     */
    public TreeNode increasingBST(TreeNode root) {
        List<TreeNode> list = new ArrayList<>();
        dfs(root, list);
        for (int i = 0; i < list.size() - 1; i++) {
            list.get(i).left = null;
            list.get(i).right = list.get(i+1);
        }
        list.get(list.size() - 1).left = null;
        list.get(list.size() - 1).right = null;
        return list.get(0);
    }
    public void dfs(TreeNode root, List<TreeNode> list) {
        if (root == null) {return;}
        dfs(root.left, list);
        list.add(root);
        dfs(root.right, list);
    }
}

```

## B

```text
public class Solution {
    /*
    Runtime: 1 ms, faster than 6.44% of Java online submissions for Increasing Order Search Tree.
    Memory Usage: 36.6 MB, less than 50.83% of Java online submissions for Increasing Order Search Tree.
     */
    public TreeNode increasingBST(TreeNode root) {
        List<TreeNode> list = bfsInorder(root);
        for (int i = 0; i < list.size() - 1; i++) {
            list.get(i).left = null;
            list.get(i).right = list.get(i+1);
        }
        list.get(list.size() - 1).left = null;
        list.get(list.size() - 1).right = null;
        return list.get(0);
    }
    public List<TreeNode> bfsInorder(TreeNode root) {
        // 尽量向左子节点前进
        // 途中经过的父节点先存在一个Stack中
        // 等到没有更多左子节点时, 取出Stack中的父节点并拜访其右子节点
        List<TreeNode> res = new LinkedList<>();
        if (root == null) {return res;}

        Deque<TreeNode> stack = new LinkedList<>();
        TreeNode cur = root;

        while(cur != null || !stack.isEmpty()){
            if (cur != null) {
                stack.push(cur);
                cur = cur.left;
            }
            if (cur == null){
                TreeNode node = stack.pop();
                res.add(node);
                cur = node.right;
            }
        }

        return res;
    }
}
```

