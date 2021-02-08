---
description: DFS ~ Recursive
---

# DFSTemplate

## DFSTemplate

```text
class DFSTemplate {
    // dfs basic
    public void dfs(TreeNode root) {
        if (root == null) {
            return;
        }
        dfs(root.left);
        dfs(root.right);
    }

    // dfs boolean
    public boolean dfs(TreeNode root, int value) {
        if (root.val != value) {
            return false;
        }
        boolean left = true;
        boolean right = true;
        if (root.left != null) {
            left = dfs(root.left, value);
        }
        if (root.right != null) {
            right = dfs(root.right, value);
        }
        return left && right;
    }
}
```

## DFSLevelOrder

```text
class DFSLevelOrder {
    public List<List<Integer>> levelOrder(TreeNode root) {
        dfs(root, 0);
        return result;
    }
    List<List<Integer>> result = new LinkedList<>();
    private void dfs(TreeNode root, int depth) {
        if (root == null) {return;}
        if (result.size() == depth) {
            result.add(new LinkedList<>());
        }
        result.get(depth).add(root.val);
        dfs(root.left, depth+1);
        dfs(root.right, depth+1);
    }
}
```

