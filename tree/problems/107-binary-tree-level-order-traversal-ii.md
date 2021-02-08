---
description: Easy
---

# 107 Binary Tree Level Order Traversal II

```text
// Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

// For example:
// Given binary tree [3,9,20,null,null,15,7],
// return its bottom-up level order traversal as:
// [
//   [15,7],
//   [9,20],
//   [3]
// ]
```

## A

```text
class Solution {
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        //BFS
        //List<List<Integer>>
        List<List<Integer>> ll = new LinkedList<>();
        Queue<TreeNode> queue = new LinkedList<>();
        if(root != null) queue.add(root);
        while(!queue.isEmpty()){
            int size = queue.size();
            List<Integer> l = new LinkedList<>();
            for(int i=0; i<size; i++){
                TreeNode temp = queue.poll();
                l.add(temp.val);
                if(temp.left != null) queue.add(temp.left);
                if(temp.right != null) queue.add(temp.right);
            }
            ll.add(0, l);
        }
        return ll;
    }
}
```

## B

```text
class Solution {
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        //DFS, helper()
        //List<List<Integer>>       
        helper(root, 0);
        return ll;
    }

    List<List<Integer>> ll = new LinkedList<>();
    private void helper(TreeNode node, int level){
        if(node == null) return;
        if(ll.size() == level){
            ll.add(0, new LinkedList<>());
        }
        ll.get(ll.size() -1 - level).add(node.val);
        helper(node.left, level+1);
        helper(node.right, level+1);
    }
}
```

## C

```text
class Solution {
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        //BFS
        //List<List<Integer>>
        List<List<Integer>> ll = new LinkedList<>();
        Queue<TreeNode> queue = new LinkedList<>();
        if(root != null) queue.add(root);
        while(!queue.isEmpty()){
            int size = queue.size();
            List<Integer> l = new LinkedList<>();
            for(int i=0; i<size; i++){
                TreeNode temp = queue.poll();
                l.add(temp.val);
                if(temp.left != null) queue.add(temp.left);
                if(temp.right != null) queue.add(temp.right);
            }
            ll.add(l);
        }
        Collections.reverse(ll);
        return ll;
    }
}
```

