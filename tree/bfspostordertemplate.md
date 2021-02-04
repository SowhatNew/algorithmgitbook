# BFSPostorderTemplate

```text
class BFSPostorderTemplate {
    // bfs postorder binary tree
    public int bfsPostorderBT(TreeNode root) {
        if (root == null) {return 0;}
        int res = 0;
        int curSum = 0;
        Deque<TreeNode> stack = new LinkedList<>();
        TreeNode cur = root;
        TreeNode pre = null;
        while (cur != null || !stack.isEmpty()) {
            while (cur != null) {
                curSum = curSum * 10 + cur.val;
                stack.push(cur);
                cur = cur.left;
            }
            cur = stack.peek();
            if (cur.left == null && cur.right == null) {
                res += curSum;
            }
            if (cur.right == null || cur.right == pre) {
                curSum = (curSum - cur.val) / 10;
                stack.pop();
                pre = cur;
                cur = null;
            } else {
                cur = cur.right;
            }
        }
        return res;
    }


    // bfs postorder binary tree
    public List<Integer> bfsPostorderBT2(TreeNode root) {
        if (root == null) {
            return Collections.emptyList();
        }

        LinkedList<Integer> res = new LinkedList<>();
        Deque<TreeNode> stack = new ArrayDeque<>();
        stack.push(root);

        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            if (node.left != null) {
                stack.push(node.left);
            }
            if (node.right != null) {
                stack.push(node.right);
            }
            res.addFirst(node.val);
        }

        return res;
    }


    // bfs postorder n-ary tree
    public List<Integer> bfsPostorderNAryTree(Node root) {
        if (root == null) {
            return Collections.emptyList();
        }

        LinkedList<Integer> res = new LinkedList<>();
        Deque<Node> stack = new ArrayDeque<>();
        stack.push(root);

        while (!stack.isEmpty()) {
            Node node = stack.pop();
            node.children.forEach(stack::push);
            res.addFirst(node.val);
        }

        return res;
    }
}
```

