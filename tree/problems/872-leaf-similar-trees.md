---
description: Easy
---

# 872 Leaf-Similar Trees

```text
//Consider all the leaves of a binary tree, from left to right order,
// the values of those leaves form a leaf value sequence.
//Constraints:
//The number of nodes in each tree will be in the range [1, 200].
//Both of the given trees will have values in the range [0, 200].
//For example, in the given tree above, the leaf value sequence is (6, 7, 4, 9, 8).
//Two binary trees are considered leaf-similar if their leaf value sequence is the same.
//Return true if and only if the two given trees with head nodes root1 and root2 are leaf-similar.
```

## A

```text
public class Solution {
    public boolean leafSimilar(TreeNode root1, TreeNode root2) {
        List<Integer> list1 = new ArrayList<>();
        List<Integer> list2 = new ArrayList<>();
//        dfs(root1, list1);
//        dfs(root2, list2);
        bfs(root1, list1);
        bfs(root2, list2);
        if (list1.size() != list2.size()) {return false;}
        for (int i = 0; i < list1.size(); i++) {
            if (!list1.get(i).equals(list2.get(i))) {return false;}
        }
        return true;
    }
}
```

## B

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Leaf-Similar Trees.
    Memory Usage: 36.7 MB, less than 77.24% of Java online submissions for Leaf-Similar Trees.
     */    
    public void dfs(TreeNode root, List<Integer> list) {
        if (root == null) {return;}
        if (root.left == null && root.right == null) {list.add(root.val);}
        dfs(root.left, list);
        dfs(root.right, list);
    }
}
```

## C

```text
public class Solution {
    /*
    Runtime: 1 ms, faster than 19.91% of Java online submissions for Leaf-Similar Trees.
    Memory Usage: 36.7 MB, less than 77.24% of Java online submissions for Leaf-Similar Trees.
     */
    public void bfs(TreeNode root, List<Integer> list) {
        if (root == null) {return;}

        Deque<TreeNode> stack = new LinkedList<>();
        stack.push(root);

        while(!stack.isEmpty()){
            TreeNode node = stack.pop();
            if (node == null) {continue;}
            if (node.left == null && node.right == null) {list.add(node.val);}
            stack.push(node.right);
            stack.push(node.left);
        }
    }
}
```

