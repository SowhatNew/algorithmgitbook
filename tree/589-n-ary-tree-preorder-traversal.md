---
description: Easy
---

# 589 N-ary Tree Preorder Traversal

```text
//Given an n-ary tree, return the preorder traversal of its nodes' values.
//Nary-Tree input serialization is represented in their level order traversal,
// each group of children is separated by the null value (See examples).

//Follow up:
//Recursive solution is trivial, could you do it iteratively?
```

## A

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for N-ary Tree Preorder Traversal.
    Memory Usage: 39.5 MB, less than 77.84% of Java online submissions for N-ary Tree Preorder Traversal.
     */
    List<Integer> list = new LinkedList<>();
    public List<Integer> preorder(Node root) {
        dfs(root);
        return list;
    }
    public void dfs(Node root) {
        if (root == null) {return;}
        list.add(root.val);
        for (Node node : root.children) {
            dfs(node);
        }
    }
}
```

## B

```text
class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for N-ary Tree Preorder Traversal.
	Memory Usage: 40.5 MB, less than 7.86% of Java online submissions for N-ary Tree Preorder Traversal.
	*/
    public List<Integer> list = new ArrayList<>();
    public List<Integer> preorder(Node root) {
        if (root == null) {return list;}
        
        list.add(root.val);
        for(Node node: root.children) {
            preorder(node);
        }     
        return list;
    }
}
```

## C

```text
public class Solution {
    /*
    Runtime: 2 ms, faster than 45.96% of Java online submissions for N-ary Tree Preorder Traversal.
    Memory Usage: 40.4 MB, less than 7.86% of Java online submissions for N-ary Tree Preorder Traversal.
     */
    public List<Integer> preorder(Node root) {
        List<Integer> list = new LinkedList<>();
        if (root == null) {return list;}

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

