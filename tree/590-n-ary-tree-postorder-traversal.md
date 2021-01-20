---
description: Easy
---

# 590 N-ary Tree Postorder Traversal

```text
//Given an n-ary tree, return the postorder traversal of its nodes' values.
//Nary-Tree input serialization is represented in their level order traversal, 
// each group of children is separated by the null value (See examples).
//Follow up:
//Recursive solution is trivial, could you do it iteratively?
```

## A

```text
class Solution {
    /*
    Runtime: 1 ms, faster than 57.16% of Java online submissions for N-ary Tree Postorder Traversal.
    Memory Usage: 40.1 MB, less than 33.52% of Java online submissions for N-ary Tree Postorder Traversal.
     */
    List<Integer> list = new LinkedList<>();
    public List<Integer> postorder(Node root) {
        if (root == null) {return list;}
        for (Node node : root.children) {
            postorder(node);
        }
        list.add(root.val);
        return list;
    }
}
```

## B

```text
public class Solution {
    /*
    Runtime: 3 ms, faster than 27.88% of Java online submissions for N-ary Tree Postorder Traversal.
    Memory Usage: 39.8 MB, less than 72.63% of Java online submissions for N-ary Tree Postorder Traversal.
     */
    public List<Integer> postorder(Node root) {
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

## C

```text
public class Solution {
    /*
    Runtime: 3 ms, faster than 27.88% of Java online submissions for N-ary Tree Postorder Traversal.
    Memory Usage: 39.7 MB, less than 72.63% of Java online submissions for N-ary Tree Postorder Traversal.
     */
    public List<Integer> postorder(Node root) {
        List<Integer> res = new LinkedList<>();
        if (root == null) {return res;}

        Deque<Node> s = new LinkedList<>();
        if (root != null) {s.push(root);}
        while (! s.isEmpty()) {
            Node node = s.pop();
            res.add(node.val);
            for (Node e : node.children) {
                s.push(e);
            }
        }
        Collections.reverse(res);
        return res;
    }
}
```

