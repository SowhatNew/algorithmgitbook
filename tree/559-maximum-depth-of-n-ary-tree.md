---
description: Easy
---

# 559 Maximum Depth of N-ary Tree

```text
//Given a n-ary tree, find its maximum depth.
//The maximum depth is the number of nodes along the longest path 
// from the root node down to the farthest leaf node.
//Nary-Tree input serialization is represented in their level order traversal, 
// each group of children is separated by the null value (See examples).
```

## A

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Maximum Depth of N-ary Tree.
    Memory Usage: 41.1 MB, less than 5.01% of Java online submissions for Maximum Depth of N-ary Tree.
     */
    public int maxDepth(Node root) {
        if (root == null) {return 0;}
        int max = 0;
        for (Node node: root.children) {
            max = Math.max(max, maxDepth(node));
        }
        return max + 1;
    }
}
```

## B

```text
public class Solution {
    /*
    Runtime: 5 ms, faster than 6.40% of Java online submissions for Maximum Depth of N-ary Tree.
    Memory Usage: 41.8 MB, less than 5.01% of Java online submissions for Maximum Depth of N-ary Tree.
     */
    public int maxDepth(Node root) {
        if (root == null) {return 0;}

        int depth = 0;
        Queue<Node> q = new LinkedList<>();
        q.offer(root);
        while(!q.isEmpty()){
            int size = q.size();
            for(int i = 0;  i < size; i++){
                Node temp = q.poll();
                for (Node node : temp.children){
                    q.offer(node);
                }
            }
            depth++;
        }
        return depth;
    }
}
```

