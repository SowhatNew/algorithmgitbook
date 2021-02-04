# BFSPreorderTemplate

```text
class BFSPreorderTemplate {
    // bfs preorder binary tree
    public List<Integer> bfsPreorderBT(TreeNode root) {
        List<Integer> list = new LinkedList<>();

        if (root == null) {
            return list;
        }

        Deque<TreeNode> stack = new LinkedList<>();
        stack.push(root);

        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            list.add(node.val);
            if (node.right != null) {
                stack.push(node.right);
            }
            if (node.left != null) {
                stack.push(node.left);
            }
        }
        return list;
    }


    // bfs preorder n-ary tree
    public List<Integer> bfsPreorderNAryTree(Node root) {
        List<Integer> list = new LinkedList<>();

        if (root == null) {
            return list;
        }

        Deque<Node> stack = new LinkedList<>();
        stack.push(root);

        while (!stack.isEmpty()) {
            Node node = stack.pop();
            list.add(node.val);
            for (int i = node.children.size() - 1; i >= 0; i--) {
                stack.push(node.children.get(i));
            }
        }
        return list;
    }
}
```

