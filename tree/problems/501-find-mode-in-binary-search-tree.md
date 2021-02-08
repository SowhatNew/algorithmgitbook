---
description: Easy
---

# 501 Find Mode in Binary Search Tree

```text
//Given a binary search tree (BST) with duplicates, find all the mode(s) 
// (the most frequently occurred element) in the given BST.
//Assume a BST is defined as follows:
//The left subtree of a node contains only nodes with keys less than or equal to the node's key.
//The right subtree of a node contains only nodes with keys greater than or equal to the node's key.
//Both the left and right subtrees must also be binary search trees.
//[1,null,2] -> [1,2]
//[1,null,2,2] -> [2]
```

## A

```text
class Solution {
    /*
    Runtime: 3 ms, faster than 53.66% of Java online submissions for Find Mode in Binary Search Tree.
	Memory Usage: 40.3 MB, less than 52.93% of Java online submissions for Find Mode in Binary Search Tree.
	*/
    HashMap<Integer, Integer> map = new HashMap<>();
    int cntAtThisMode = 0;
    int maxMode = 0;
    
    public int[] findMode(TreeNode root) {
        dfs(root);
        
        int[] res = new int[this.cntAtThisMode];
        int i = -1;
                
        for (int key : map.keySet())
            if (map.get(key) == this.maxMode)
                res[++i] = key;
        
        return res;
    }
    
    public void dfs(TreeNode root) {
        if (root == null)
            return;
        
        int modeOfThisNum = this.map.containsKey(root.val) ? this.map.get(root.val) + 1 : 1;
        this.map.put(root.val, modeOfThisNum);
        
        if (modeOfThisNum == this.maxMode)
            this.cntAtThisMode++;
        else if (modeOfThisNum > this.maxMode) {
            this.cntAtThisMode = 1; // only one value has this mode now
            this.maxMode++;
        }
        
        dfs(root.left);
        dfs(root.right);
    }
}
```

## B

```text
public class Solution {
    /*
    Runtime: 13 ms, faster than 5.37% of Java online submissions for Find Mode in Binary Search Tree.
    Memory Usage: 40.1 MB, less than 56.76% of Java online submissions for Find Mode in Binary Search Tree.
     */
    TreeMap<Integer, Integer> map = new TreeMap<>();
    public int[] findMode(TreeNode root) {
        dfs(root);

        List<Integer> list = new ArrayList<>();
        int max = Integer.MIN_VALUE;
        for (int key : map.keySet()) {
            if (map.get(key) > max) {
                list.clear();
                max = map.get(key);
                list.add(key);
            } else if (max == map.get(key)) {
                list.add(key);
            }
        }
        return list.stream().mapToInt(i->i).toArray();
    }
    public void dfs(TreeNode root) {
        if (root == null) {return;}
        int modeOfThisNum = this.map.containsKey(root.val) ? this.map.get(root.val) + 1 : 1;
        this.map.put(root.val, modeOfThisNum);
        dfs(root.left);
        dfs(root.right);
    }
}
```

