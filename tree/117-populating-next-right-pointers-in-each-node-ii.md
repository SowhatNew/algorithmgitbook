---
description: Medium
---

# 117 Populating Next Right Pointers in Each Node II

```text
//Given a binary tree
//Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL.
//Initially, all next pointers are set to NULL.
//Follow up:
//You may only use constant extra space.
//Recursive approach is fine, you may assume implicit stack space does not count as extra space for this problem.
```

## A

```text
public class Solution {
    /*
    Runtime: 1 ms, faster than 60.95% of Java online submissions for Populating Next Right Pointers in Each Node II.
    Memory Usage: 41.6 MB, less than 16.93% of Java online submissions for Populating Next Right Pointers in Each Node II.
     */
    public Node connect(Node root) {
        Node cur = root;
        while (cur != null) {
            Node dummy= new Node();
            Node tail = dummy;
            while (cur != null) {
                if (cur.left != null) {
                    tail.next = cur.left;
                    tail = tail.next;
                }
                if (cur.right != null) {
                    tail.next = cur.right;
                    tail = tail.next;
                }
                cur = cur.next;
            }
            cur = dummy.next;
        }
        return root;
    }   
}    
```

## B

```text
public class Solution {
    /*
    Runtime: 1 ms, faster than 60.95% of Java online submissions for Populating Next Right Pointers in Each Node II.
    Memory Usage: 38.8 MB, less than 49.03% of Java online submissions for Populating Next Right Pointers in Each Node II.
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

