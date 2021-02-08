---
description: BFS ~ Iterative
---

# BFSTemplate

```text
class BFSTemplate {
    // bfs queue
    public TreeNode bfsQueue(TreeNode root, int val) {
        if (root == null) {
            return null;
        }

        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);

        while (!queue.isEmpty()) {
            TreeNode node = queue.poll();
            if (node == null) {
                continue;
            }
            if (node.val == val) {
                return node;
            }
            queue.offer(node.left);
            queue.offer(node.right);
        }

        return null;
    }

    // bfs stack
    public void bfsStack(TreeNode root, List<Integer> list) {
        if (root == null) {
            return;
        }

        Deque<TreeNode> stack = new LinkedList<>();
        stack.push(root);

        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            if (node == null) {
                continue;
            }
            if (node.left == null && node.right == null) {
                list.add(node.val);
            }
            stack.push(node.right);
            stack.push(node.left);
        }
    }

    // bfs level-order size
    public int calcMaxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }

        int depth = 0;
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);

        while (!q.isEmpty()) {
            int size = q.size();
            for (int i = 0; i < size; i++) {
                TreeNode node = q.poll();
                if (node.left != null) {
                    q.add(node.left);
                }
                if (node.right != null) {
                    q.add(node.right);
                }
            }
            depth++;
        }
        return depth;
    }
}
```

