# BFSInorderTemplate

```text
class BFSInorderTemplate {
    // bfs inorder binary tree
    public List<TreeNode> bfsInorderBT(TreeNode root) {
        List<TreeNode> res = new LinkedList<>();

        if (root == null) {
            return res;
        }

        Deque<TreeNode> stack = new LinkedList<>();
        TreeNode cur = root;

        while (cur != null || !stack.isEmpty()) {
            while (cur != null) {
                stack.push(cur);
                cur = cur.left;
            }
            TreeNode node = stack.pop();
            res.add(node);
            cur = node.right;
        }

        return res;
    }
}
```

