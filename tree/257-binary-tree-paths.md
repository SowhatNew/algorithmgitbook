---
description: Easy
---

# 257 Binary Tree Paths

```text
// Given a binary tree, return all root-to-leaf paths.
// Note: A leaf is a node with no children.

// Example:
// Input:
//    1
//  /   \
// 2     3
//  \
//   5
// Output: ["1->2->5", "1->3"]
// Explanation: All root-to-leaf paths are: 1->2->5, 1->3
```

## A

```text
class Solution {
    private List<String> lStrings;
    public List<String> binaryTreePaths(TreeNode root) {
        lStrings = new LinkedList<>();
        dfs(root, new StringBuffer());
        return lStrings;
    }
    private void dfs(TreeNode node, StringBuffer buffer){
        if(node == null) return;
        buffer.append(node.val);
        if((node.left == null) && (node.right == null)){
            lStrings.add(buffer.toString());
        }
        buffer.append("->");
        if(node.left != null) {            
            dfs(node.left, new StringBuffer(buffer));
        }
        if(node.right != null){
            dfs(node.right, new StringBuffer(buffer));
        }
    }
}
```

## B

```text
class Solution2 {
    public List<String> binaryTreePaths(TreeNode root) {
        List<Integer> lIntegers = new LinkedList<>();
        helper(root, lIntegers);
        return lStrings;
    }

    List<String> lStrings = new LinkedList<>();
    private void helper(TreeNode node, List<Integer> lIntegers){
        if(node == null) return;

        lIntegers.add(node.val);
        if(node.left != null) {            
            helper(node.left, new LinkedList<>(lIntegers));
        }
        if(node.right != null){
            helper(node.right, new LinkedList<>(lIntegers));
        }
        if((node.left == null) && (node.right == null)){
            StringBuffer stringBuffer = new StringBuffer();
            for(Integer i: lIntegers){
                stringBuffer.append(i).append("->");
            }
            String s = String.valueOf(stringBuffer);
            s = s.substring(0, s.length()-2);
            lStrings.add(s);
        }
    }
}
```

## C

```text
class Solution {
    /*
    Runtime: 9 ms, faster than 25.75% of Java online submissions for Binary Tree Paths.
    Memory Usage: 39.3 MB, less than 58.84% of Java online submissions for Binary Tree Paths.
     */    
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> list=new ArrayList<String>();
        Queue<TreeNode> qNode=new LinkedList<TreeNode>();
        Queue<String> qStr=new LinkedList<String>();

        if (root==null) return list;
        qNode.add(root);
        qStr.add("");
        while(!qNode.isEmpty()) {
            TreeNode curNode=qNode.remove();
            String curStr=qStr.remove();

            if (curNode.left==null && curNode.right==null) list.add(curStr+curNode.val);
            if (curNode.left!=null) {
                qNode.add(curNode.left);
                qStr.add(curStr+curNode.val+"->");
            }
            if (curNode.right!=null) {
                qNode.add(curNode.right);
                qStr.add(curStr+curNode.val+"->");
            }
        }
        return list;
    }
}
```

