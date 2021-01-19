---
description: Medium
---

# 95 Unique Binary Search Trees II

```text
//Given an integer n, generate all structurally unique BST's (binary search trees) 
// that store values 1 ... n.
//
//Example:
//Input: 3
//Output:
//[
//  [1,null,3,2],
//  [3,2,null,1],
//  [3,1,null,null,2],
//  [2,1,3],
//  [1,null,2,null,3]
//]
```

## A

```text
public class Solution {
    /*
    Runtime: 1 ms, faster than 94.34% of Java online submissions for Unique Binary Search Trees II.
    Memory Usage: 39.4 MB, less than 76.69% of Java online submissions for Unique Binary Search Trees II.
     */
    public List<TreeNode> generateTrees(int n) {
        if (n == 0) {
            return new ArrayList<>();
        }
        return generateTrees(1, n);
    }

    private List<TreeNode> generateTrees(int lo, int hi) {
        int n = hi - lo + 1;
        if (n == 0) {
            List<TreeNode> L = new ArrayList<>();
            L.add(null); 
            return L;
        }
        List<TreeNode> result = new ArrayList<>();
        for (int i = lo; i <= hi; ++i) {
            List<TreeNode> leftSubtrees = generateTrees(lo, i - 1);
            List<TreeNode> rightSubtrees = generateTrees(i + 1, hi);
            for (TreeNode leftSub : leftSubtrees) {
                for (TreeNode rightSub : rightSubtrees) {
                    TreeNode newTree = new TreeNode(i);
                    newTree.left = leftSub;
                    newTree.right = rightSub;
                    result.add(newTree);
                }
            }
        }
        return result;
    }

}
```

## B

```text
public class Solution {
    /*
    Runtime: 1 ms, faster than 94.34% of Java online submissions for Unique Binary Search Trees II.
    Memory Usage: 39.8 MB, less than 46.21% of Java online submissions for Unique Binary Search Trees II.
     */
    public List<TreeNode> generateTrees(int n) {
        List<TreeNode> result = new LinkedList<>();
        if (n < 1) {return result;}
        result = dfs(1, n);
        return result;
    }
    private List<TreeNode> dfs(int min, int max) {
        List<TreeNode> listRoot = new LinkedList<>();
        if (min > max) {
            return listRoot;
        }
        if (min == max) {
            listRoot.add(new TreeNode(min));
            return listRoot;
        }
        for (int i = min; i <= max; i++) {
            List<TreeNode> listLeft = null;
            List<TreeNode> listRight = null;
            if ((i-1) >= min) {
                listLeft = dfs(min, i-1);
            }
            if ((i+1) <= max) {
                listRight = dfs(i+1, max);
            }
            if (listLeft != null && listRight != null) {
                for (TreeNode left : listLeft) {
                    for (TreeNode right : listRight) {
                        TreeNode node = new TreeNode(i);
                        node.left = left;
                        node.right = right;
                        listRoot.add(node);
                    }
                }
            } else if (listLeft != null){
                for (TreeNode left : listLeft) {
                    TreeNode node = new TreeNode(i);
                    node.left = left;
                    node.right = null;
                    listRoot.add(node);
                }
            } else if (listRight != null) {
                for (TreeNode right : listRight) {
                    TreeNode node = new TreeNode(i);
                    node.left = null;
                    node.right = right;
                    listRoot.add(node);
                }
            }

        }
        return listRoot;
    }
}

```

## C

```text
public class Solution {
    /*
    Runtime: 1 ms, faster than 94.34% of Java online submissions for Unique Binary Search Trees II.
    Memory Usage: 39.4 MB, less than 83.49% of Java online submissions for Unique Binary Search Trees II.
     */
    private TreeNode clone(TreeNode root, int offset) {
        if (root == null) {
            return null;
        }
        TreeNode node = new TreeNode(root.val + offset);
        node.left = clone(root.left, offset);
        node.right = clone(root.right, offset);
        return node;
    }
    public List<TreeNode> generateTrees(int n) {
        List<TreeNode>[] tree = new ArrayList[n + 1];
        tree[0] = new ArrayList<>();
        if (n == 0) {
            return tree[0];
        }
        tree[0].add(null);
        // Calculate all lengths
        for (int len = 1; len <= n; ++len) {
            tree[len] = new ArrayList<>(); // contains all trees we construct
            // Consider each as the root
            for (int i = 1; i <= len; ++i) {
                int leftSize = i - 1;
                int rightSize = len - i;
                for (TreeNode leftTree : tree[leftSize]) {
                    for (TreeNode rightTree : tree[rightSize]) {
                        TreeNode node = new TreeNode(i);
                        node.left = leftTree;  // left subtree requires no cloning
                        node.right = clone(rightTree, i); // add i as the offset
                        tree[len].add(node);
                    }
                }
            }
        }
        return tree[n];
    }

}
```

## D

```text
public class Solution {
    /*
    Runtime: 1 ms, faster than 94.34% of Java online submissions for Unique Binary Search Trees II.
    Memory Usage: 39.2 MB, less than 88.28% of Java online submissions for Unique Binary Search Trees II.
     */
    public List<TreeNode> generateTrees(int n) {
        if (n == 0) {
            return new ArrayList<>();
        }
        List<TreeNode>[][] g = new ArrayList[n + 1][n + 1];
        // init
        List<TreeNode> nullList = new ArrayList<>(); nullList.add(null);
        g[0][0] = nullList;
        for (int k = 1; k <= n; ++k) { // g(0, k)
            g[0][k] = nullList;
        }
        for (int k = 1; k <= n; ++k) { // diagonal: one node (itself)
            List<TreeNode> oneList = new ArrayList<>(); oneList.add(new TreeNode(k));
            g[k][k] = oneList;
        }
        for (int k = 1; k <= n; ++k) { // one node above diagonal: nullList
            g[k][k - 1] = nullList;
        }
        // dp
        for (int i = n - 1; i >= 1; --i) {
            for (int j = i + 1; j <= n; ++j) {
                List<TreeNode> result = new ArrayList<>();
                for (int k = i ; k <= j; ++k) { // for each k as root [i, j]
                    List<TreeNode> leftList = (k - 1 <= n) ? g[i][k - 1] : nullList;
                    List<TreeNode> rightList = (k + 1 <= n) ? g[k + 1][j] : nullList;
                    for (TreeNode left : leftList) {
                        for (TreeNode right: rightList) {
                            TreeNode newTree = new TreeNode(k);
                            newTree.left = left;
                            newTree.right = right;
                            result.add(newTree);
                        }
                    }
                }
                g[i][j] = result;
            }
        }
        return g[1][n];
    }
}
```

