---
description: Medium
---

# 429 N-ary Tree Level Order Traversal

```text
Given an n-ary tree, return the level order traversal of its nodes' values.

Nary-Tree input serialization is represented in their level order traversal, 
each group of children is separated by the null value (See examples).

Constraints:
The height of the n-ary tree is less than or equal to 1000
The total number of nodes is between [0, 104]
```

```text
public class Solution {
    /*
    Runtime: 2 ms, faster than 85.90% of Java online submissions for N-ary Tree Level Order Traversal.
    Memory Usage: 39.8 MB, less than 65.15% of Java online submissions for N-ary Tree Level Order Traversal.
     */
    public List<List<Integer>> levelOrder(Node root) {
        List<List<Integer>> res = new LinkedList<>();
        if (root == null) {return res;}

        Queue<Node> queue = new LinkedList<>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            int size = queue.size();
            List<Integer> list = new ArrayList<>();
            for (int i = 0; i < size; i++) {
                Node node = queue.poll();
                list.add(node.val);
                node.children.forEach(queue::offer);
            }
            res.add(list);
        }
        return res;
    }
}
```



