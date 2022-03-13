---
description: DFS ~ Recursive
---

# DFSTemplate

```java
public class DFSTemplate {
    public void dfs(TreeNode root) {
        if (root == null) {
            return;
        }
        dfs(root.left);
        dfs(root.right);
    }

    public boolean dfsSearch(TreeNode root, int value) {
        if (root == null) {
            return false;
        }
        if (root.val == value) {
            return true;
        }
        boolean left = dfsSearch(root.left, value);
        boolean right = dfsSearch(root.right, value);
        return left && right;
    }

    public List<List<Integer>> dfsLevelOrder(TreeNode root) {
        List<List<Integer>> res = new LinkedList<>();
        dfsLevelOrder(root, 0, res);
        return res;
    }
    private void dfsLevelOrder(TreeNode root, int depth, List<List<Integer>> res) {
        if (root == null) {
            return;
        }
        if (res.size() == depth) {
            res.add(new LinkedList<>());
        }
        res.get(depth).add(root.val);
        dfsLevelOrder(root.left, depth+1, res);
        dfsLevelOrder(root.right, depth+1, res);
    }
}
```



## Others
