---
description: Medium
---

# 173 Binary Search Tree Iterator

```text
//Implement the BSTIterator class that represents an iterator over the in-order traversal of a binary search tree (BST):
//
//BSTIterator(TreeNode root) Initializes an object of the BSTIterator class.
// The root of the BST is given as part of the constructor.
// The pointer should be initialized to a non-existent number smaller than any element in the BST.
//boolean hasNext() Returns true if there exists a number in the traversal to the right of the pointer,
// otherwise returns false.
//int next() Moves the pointer to the right, then returns the number at the pointer.
//Notice that by initializing the pointer to a non-existent smallest number,
// the first call to next() will return the smallest element in the BST.
//
//You may assume that next() calls will always be valid.
// That is, there will be at least a next number in the in-order traversal when next() is called.
```

## A

```text
class BSTIterator {
    /*
    Runtime: 15 ms, faster than 75.25% of Java online submissions for Binary Search Tree Iterator.
    Memory Usage: 42.7 MB, less than 86.10% of Java online submissions for Binary Search Tree Iterator.
     */
    Queue<Integer> result = new LinkedList<>();
    public BSTIterator(TreeNode root) {
        dfs(root);
    }
    private void dfs(TreeNode root) {
        if (root == null) {return;}
        dfs(root.left);
        result.offer(root.val);
        dfs(root.right);
    }

    public int next() {
        return result.poll();
    }

    public boolean hasNext() {
        return !result.isEmpty();
    }
}
```

## B

```text
class BSTIterator {
    /*
    Runtime: 16 ms, faster than 37.17% of Java online submissions for Binary Search Tree Iterator.
    Memory Usage: 43.1 MB, less than 35.64% of Java online submissions for Binary Search Tree Iterator.
     */
    Queue<Integer> result = new LinkedList<>();
    public BSTIterator(TreeNode root) {
        Deque<TreeNode> stack = new ArrayDeque<>();
        TreeNode p = root;
        while(!stack.isEmpty() || p != null) {
            if(p != null) {
                stack.push(p);
                p = p.left;
            } else {
                TreeNode node = stack.pop();
                result.offer(node.val);  // Add after all left children
                p = node.right;
            }
        }
    }

    public int next() {
        return result.poll();
    }

    public boolean hasNext() {
        return !result.isEmpty();
    }
}
```

