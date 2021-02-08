---
description: Medium
---

# 116 Populating Next Right Pointers in Each Node

```text
//You are given a perfect binary tree where all leaves are on the same level, 
// and every parent has two children. 
// The binary tree has the following definition:
//Populate each next pointer to point to its next right node. 
// If there is no next right node, the next pointer should be set to NULL.
//
//Initially, all next pointers are set to NULL.
//
//
//
//Follow up:
//You may only use constant extra space.
//Recursive approach is fine,
// you may assume implicit stack space does not count as extra space for this problem.
​
class Node {
    public int val;
    public Node left;
    public Node right;
    public Node next;
​
    public Node() {
    }
​
    public Node(int _val) {
        val = _val;
    }
​
    public Node(int _val, Node _left, Node _right, Node _next) {
        val = _val;
        left = _left;
        right = _right;
        next = _next;
    }
}
```

## A

```text
public class Solution {
    /*
    Runtime: 2 ms, faster than 44.92% of Java online submissions for Populating Next Right Pointers in Each Node.
    Memory Usage: 39.5 MB, less than 28.92% of Java online submissions for Populating Next Right Pointers in Each Node.
     */
    public Node connect(Node root) {
        if (root == null) {
            return root;
        }
        connectTwoNode(root.left, root.right);
        return root;
    }
    private void connectTwoNode(Node node1, Node node2){
        if (node1 == null || node2 == null) {
            return;
        }
        node1.next = node2;
        connectTwoNode(node1.left, node1.right);
        connectTwoNode(node1.right, node2.left);
        connectTwoNode(node2.left, node2.right);
    }
}
```

## B

```text
public class Solution {
    /*
    Runtime: 1 ms, faster than 56.81% of Java online submissions for Populating Next Right Pointers in Each Node.
    Memory Usage: 39 MB, less than 89.45% of Java online submissions for Populating Next Right Pointers in Each Node.
         */
    public Node connect(Node root) {
        if (root == null) {
            return root;
        }
        Queue<Node> queue = new LinkedList<>();
        queue.offer(root);
        Node pre = null;
        while (!queue.isEmpty()) {
            int size = queue.size();
            pre = null;
            for (int i = 0; i < size; i++) {
                Node node = queue.poll();
                node.next = pre;
                pre = node;
                if (node.right != null) {
                    queue.offer(node.right);
                }
                if (node.left != null) {
                    queue.offer(node.left);
                }
            }
        }
        return root;
    }
}
```

## C

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Populating Next Right Pointers in Each Node.
    Memory Usage: 38.9 MB, less than 95.40% of Java online submissions for Populating Next Right Pointers in Each Node.
     */
    public Node connect(Node root) {
        if (root == null) {
            return root;
        }
        Node pre = root;
        Node cur = null;
        Node start = pre;
        while (pre.left != null) {
            if (cur == null) {
                pre.left.next = pre.right;
                pre = start.left;
                cur = start.right;
                start = pre;
            } else {
                pre.left.next = pre.right;
                pre.right.next = cur.left;
                pre = pre.next;
                cur = cur.next;
            }
        }
        return root;
    }
}
```

