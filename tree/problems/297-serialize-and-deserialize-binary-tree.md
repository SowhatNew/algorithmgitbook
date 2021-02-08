---
description: Hard
---

# 297\* Serialize and Deserialize Binary Tree

```text
Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, 
or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. 
There is no restriction on how your serialization/deserialization algorithm should work. 
You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

Constraints:
The number of nodes in the tree is in the range [0, 104].
-1000 <= Node.val <= 1000
```

## A

```text
public class CodecPreorder {
    /*
    Runtime: 7 ms, faster than 91.84% of Java online submissions for Serialize and Deserialize Binary Tree.
    Memory Usage: 40.8 MB, less than 76.38% of Java online submissions for Serialize and Deserialize Binary Tree.
     */
    private final String SEP = ",";
    private final String NULL = "#";

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        StringBuffer sb = new StringBuffer();
        serializeDFS(root, sb);
        return sb.substring(0, sb.length()-1);
    }

    private void serializeDFS(TreeNode root, StringBuffer sb) {
        if (root == null) {
            sb.append(NULL).append(SEP);
            return;
        }

        sb.append(root.val).append(SEP);
        serializeDFS(root.left, sb);
        serializeDFS(root.right, sb);
    }


    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        Queue<String> queue = new LinkedList<>();
        for (String s : data.split(SEP)) {
            queue.offer(s);
        }
        return deserializeDFS(queue);
    }

    private TreeNode deserializeDFS(Queue<String> queue) {
        if (queue.isEmpty()) {
            return null;
        }

        String val = queue.poll();
        if (val.equals(NULL)) {
            return null;
        }

        TreeNode root = new TreeNode(Integer.parseInt(val));
        root.left = deserializeDFS(queue);
        root.right = deserializeDFS(queue);

        return root;
    }
}
```

## B

```text
public class CodecPostorder {
    /*
    Runtime: 7 ms, faster than 91.84% of Java online submissions for Serialize and Deserialize Binary Tree.
    Memory Usage: 40.9 MB, less than 76.38% of Java online submissions for Serialize and Deserialize Binary Tree.
     */
    private final String SEP = ",";
    private final String NULL = "#";

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        StringBuffer sb = new StringBuffer();
        serializeDFS(root, sb);
        return sb.substring(0, sb.length()-1);
    }

    private void serializeDFS(TreeNode root, StringBuffer sb) {
        if (root == null) {
            sb.append(NULL).append(SEP);
            return;
        }

        serializeDFS(root.left, sb);
        serializeDFS(root.right, sb);
        sb.append(root.val).append(SEP);
    }


    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        Deque deque = new LinkedList();
        for (String s : data.split(SEP)) {
            deque.offer(s);
        }
        return deserializeDFS(deque);
    }

    private TreeNode deserializeDFS(Deque<String> deque) {
        if (deque.isEmpty()) {
            return null;
        }

        String val = deque.pollLast();
        if (val.equals(NULL)) {
            return null;
        }

        TreeNode root = new TreeNode(Integer.parseInt(val));
        root.right = deserializeDFS(deque);
        root.left = deserializeDFS(deque);

        return root;
    }
}
```

## C

```text
public class CodecLevelorder {
    /*
    Runtime: 11 ms, faster than 66.25% of Java online submissions for Serialize and Deserialize Binary Tree.
    Memory Usage: 40.1 MB, less than 98.93% of Java online submissions for Serialize and Deserialize Binary Tree.
     */
    private final String SEP = ",";
    private final String NULL = "#";

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        if (root == null) {
            return "";
        }

        StringBuilder sb = new StringBuilder();
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            TreeNode node = queue.poll();
            if (node == null) {
                sb.append(NULL).append(SEP);
                continue;
            }
            sb.append(node.val).append(SEP);
            queue.offer(node.left);
            queue.offer(node.right);
        }

        return sb.substring(0, sb.length()-1);
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        if (data.isEmpty()) {
            return null;
        }

        String[] nodes = data.split(SEP);
        TreeNode root = new TreeNode(Integer.parseInt(nodes[0]));
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        for (int i = 1; i < nodes.length; ) {
            TreeNode parent = queue.poll();

            String left = nodes[i++];
            if (!left.equals(NULL)) {
                parent.left = new TreeNode(Integer.parseInt(left));
                queue.offer(parent.left);
            } else {
                parent.left = null;
            }

            String right = nodes[i++];
            if (!right.equals(NULL)) {
                parent.right = new TreeNode(Integer.parseInt(right));
                queue.offer(parent.right);
            } else {
                parent.right = null;
            }
        }

        return root;
    }
}
```

