---
description: Easy
---

# 1022 Sum of Root To Leaf Binary Numbers

```text
//You are given the root of a binary tree where each node has a value 0 or 1.  
// Each root-to-leaf path represents a binary number starting with the most significant bit.  
// For example, if the path is 0 -> 1 -> 1 -> 0 -> 1, 
// then this could represent 01101 in binary, which is 13.
//For all leaves in the tree, consider the numbers represented by the path from the root to that leaf.
//Return the sum of these numbers. The answer is guaranteed to fit in a 32-bits integer.
```

## A

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Sum of Root To Leaf Binary Numbers.
    Memory Usage: 38.2 MB, less than 79.69% of Java online submissions for Sum of Root To Leaf Binary Numbers.
     */
    public int sumRootToLeaf(TreeNode root) {
        return sum(root, 0);
    }

    private int sum(TreeNode root, int s) {
        if(root == null) {return 0;}

        s = (s << 1) + root.val;
        if(root.left == null && root.right == null) {
            return s;
        }
        return sum(root.left, s) + sum(root.right, s);
    }
}
```

## B

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Sum of Root To Leaf Binary Numbers.
    Memory Usage: 38.4 MB, less than 68.87% of Java online submissions for Sum of Root To Leaf Binary Numbers.
     */
    public int sumRootToLeaf(TreeNode root) {
        return sum(root, 0);
    }

    private int sum(TreeNode node, int sum) {
        if (node == null) {return 0;}
        if (node.left == null && node.right == null) {return sum*2 + node.val;}
        return sum(node.left, sum*2 + node.val) + sum(node.right, sum*2 + node.val);
    }

}
```

## C

```text
public class Solution {
    /*
    Runtime: 2 ms, faster than 29.49% of Java online submissions for Sum of Root To Leaf Binary Numbers.
    Memory Usage: 38.3 MB, less than 68.87% of Java online submissions for Sum of Root To Leaf Binary Numbers.
     */
    public int sumRootToLeaf(TreeNode root) {
//        System.out.println(Integer.parseInt("0111", 2));
        sum = 0;
        dfs(root);
        return sum;
    }
    int sum = 0;
    List<Integer> list = new ArrayList<>();
    private void dfs(TreeNode root) {
        if (root == null) {return;}
        list.add(list.size(), root.val);
        if (root.left == null && root.right == null) {
            StringBuffer sb = new StringBuffer();
            for (Integer i : list) {
                sb.append(i);
            }
            sum += Integer.parseInt(sb.toString(), 2);
        } else {
            if (root.left != null) {
                bfs(root.left);
            }
            if (root.right != null) {
                bfs(root.right);
            }
        }
        list.remove(list.size()-1);
    }
}

```

## D

```text
public class Solution {
    /*
    +=  n.left.val += tmp;
    Runtime: 1 ms, faster than 43.89% of Java online submissions for Sum of Root To Leaf Binary Numbers.
    Memory Usage: 38.6 MB, less than 45.14% of Java online submissions for Sum of Root To Leaf Binary Numbers.
     */
    /*
    |=  n.left.val |= tmp;
    Runtime: 1 ms, faster than 43.89% of Java online submissions for Sum of Root To Leaf Binary Numbers.
    Memory Usage: 38.3 MB, less than 68.87% of Java online submissions for Sum of Root To Leaf Binary Numbers.
     */
    public int sumRootToLeaf(TreeNode root) {
        int sum = 0;
        if(root == null) {return sum;}

        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        while(!queue.isEmpty()) {
            int size = queue.size();
            for(int i = 0; i < size; i++) {
                TreeNode n = queue.poll();
                if(n.left == null && n.right == null) {
                    sum += n.val;
                    continue;
                }

                int tmp = (n.val << 1);
                if(n.left != null) {
                    n.left.val |= tmp; //val=0 or 1, 同 +=
                    queue.offer(n.left);
                }
                if(n.right != null) {
                    n.right.val |= tmp; //val=0 or 1, 同 +=
                    queue.offer(n.right);
                }
            }
        }
        return sum;
    }
}
```

## E

```text
public class Solution {
    /*
    Runtime: 9 ms, faster than 18.83% of Java online submissions for Sum of Root To Leaf Binary Numbers.
    Memory Usage: 38.5 MB, less than 45.14% of Java online submissions for Sum of Root To Leaf Binary Numbers.
     */
    public int sumRootToLeaf(TreeNode root) {
//        System.out.println(Integer.parseInt("0111", 2));
        return bfs(root);
    }
    private int bfs(TreeNode root) {
        if (root == null) {return 0;}

        List<TreeNode> list = new ArrayList<>();
        int sum = 0;

        Deque<TreeNode> stack = new LinkedList<>();
        stack.push(root);
        Set<TreeNode> visitedSet = new HashSet<>();
        visitedSet.add(null);

        outerwhile:while (!stack.isEmpty()) {
            Iterator<TreeNode> iterator = list.iterator();
            while (iterator.hasNext()) {
                TreeNode e = iterator.next();
                if ((e.left != null || e.right != null) &&
                    (visitedSet.contains(e.left) && visitedSet.contains(e.right))) {
                    visitedSet.add(e);
                    iterator.remove();
                    continue outerwhile;
                }
            }

            TreeNode node = stack.pop();
            list.add(list.size(), node);

            if (node.left == null && node.right == null) {
                StringBuffer sb = new StringBuffer();
                for (TreeNode e : list) {
                    sb.append(e.val);
                }
                sum += Integer.parseInt(sb.toString(), 2);
                visitedSet.add(node);
                list.remove(node);
            } else {
                if (node.right != null) {
                    stack.push(node.right);
                }
                if (node.left != null) {
                    stack.push(node.left);
                }
            }
        }
        return sum;
    }
}
```

