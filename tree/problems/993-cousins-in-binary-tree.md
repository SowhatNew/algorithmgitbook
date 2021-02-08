---
description: Easy
---

# 993 Cousins in Binary Tree

```text
//In a binary tree, the root node is at depth 0, and children of each depth k node are at depth k+1.
//Two nodes of a binary tree are cousins if they have the same depth, but have different parents.
//We are given the root of a binary tree with unique values,
// and the values x and y of two different nodes in the tree.
//Return true if and only if the nodes corresponding to the values x and y are cousins.
//Constraints:
//The number of nodes in the tree will be between 2 and 100.
//Each node has a unique integer value from 1 to 100.
```

## A

```text

public class Solution {
    TreeNode[] parents = new TreeNode[2];
    int[] levels = new int[2];
    
    public boolean isCousins(TreeNode root, int x, int y) {
        if (root == null) {return false;}
        if (root.val == x || root.val == y) {return false;}
        dfs(root, root.left, x, y, 1);
        dfs(root, root.right, x, y, 1);
//        bfs(root, x, y);
        if (levels[0] != levels[1]) {return false;}
        if (parents[0].val == parents[1].val) {return false;}
        return true;
    }

    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Cousins in Binary Tree.
    Memory Usage: 36.5 MB, less than 91.47% of Java online submissions for Cousins in Binary Tree.
     */    
    public void dfs(TreeNode parent, TreeNode node,
                    int x, int y , int level) {
        if (node == null) {return;}
        if (node.val == x) {
            levels[0] = level;
            parents[0] = parent;
        } else if (node.val == y) {
            levels[1] = level;
            parents[1] = parent;
        } else {
            dfs(node, node.left, x, y, level+1);
            dfs(node, node.right, x, y, level+1);
        }
    }
    
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Cousins in Binary Tree.
    Memory Usage: 36.7 MB, less than 67.01% of Java online submissions for Cousins in Binary Tree.
     */
    public void bfs(TreeNode root, int x, int y) {
        if (root == null) {return;}

        int depth = 0;
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);

        while(!q.isEmpty()){
            int size = q.size();
            for(int i = 0;  i < size; i++){
                TreeNode node = q.poll();
//                if (node == null) {continue;}
                bfshelper(node, node.left, q, x, y, depth);
                bfshelper(node, node.right, q, x, y, depth);
            }
            depth++;
        }
    }
    private void bfshelper(TreeNode parent, TreeNode node,
                           Queue<TreeNode> q,
                           int x, int y ,int depth) {
        if(node == null) {return;}
        q.add(node);
        if (node.val == x) {
            levels[0] = depth + 1;
            parents[0] = parent;
        }else if (node.val == y) {
            levels[1] = depth + 1;
            parents[1] = parent;
        }

    }
}
```

## B

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Cousins in Binary Tree.
    Memory Usage: 36.7 MB, less than 50.31% of Java online submissions for Cousins in Binary Tree.
     */
    public boolean isCousins(TreeNode root, int x, int y) {
        if (root == null) {return false;}

        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);

        while(!queue.isEmpty()) {
            int size = queue.size();
            boolean isXExist = false;
            boolean isYExist = false;

            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                if (node.val == x) {
                    isXExist = true;
                }
                if (node.val == y) {
                    isYExist = true;
                }

                if (node.left != null && node.right != null) {
                    if (node.left.val == x && node.right.val == y) {
                        return false;
                    }
                    if (node.right.val == x && node.left.val == y) {
                        return false;
                    }
                }
                if (node.left != null) {
                    queue.add(node.left);
                }
                if (node.right != null) {
                    queue.add(node.right);
                }
            }
            if (isXExist && isYExist) {
                return true;
            }
        }
        return false;
    }
}
```

