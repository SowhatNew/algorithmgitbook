---
description: Easy
---

# 606 Construct String from Binary Tree

```text
//You need to construct a string consists of parenthesis and integers from a binary tree with the preorder traversing way.

//The null node needs to be represented by empty parenthesis pair "()". 
//And you need to omit all the empty parenthesis pairs that don't affect the one-to-one mapping relationship between the string and the original binary tree.

// Input: Binary tree: [1,2,3,null,4]
//        1
//      /   \
//     2     3
//      \  
//       4 

// Output: "1(2()(4))(3)"
```

## A

```text
class Solution {
    public String tree2str(TreeNode t) {
        if(t==null) return "";
        if(t.left==null && t.right==null) return t.val+"";
        if(t.right==null) return t.val+"("+tree2str(t.left)+")";
        return t.val+"("+tree2str(t.left)+")("+tree2str(t.right)+")";   
    }
}
```

## B

```text
class Solution {
    public String tree2str(TreeNode t) {
        result = new StringBuffer();  
        dfs(t);
        return result.toString();
    }

    StringBuffer result;
    private void dfs(TreeNode node){
        if(node == null) {return;}
        result.append(node.val + "");
        if((node.left != null) && (node.right != null)) {
            result.append("(");
            dfs(node.left);
            result.append(")");
            result.append("(");
            dfs(node.right);
            result.append(")");
        }
        if((node.left != null) && (node.right == null)){
            result.append("(");
            dfs(node.left);
            result.append(")");
        }
        if((node.left == null) && (node.right != null)){            
            result.append("()(");
            dfs(node.right);
            result.append(")");
        }
        if((node.left == null) && (node.right != null)){
            //pass
        }
    }
}

```

## C

```text
class Solution {
    public String tree2str(TreeNode t) {
        if (t == null) {return "";}
        Stack<TreeNode> stack = new Stack<>(); {stack.push(t);}
        Set<TreeNode> visited = new HashSet<>();
        StringBuilder s = new StringBuilder();
        while (!stack.isEmpty()) {
            t = stack.peek();
            if (visited.contains(t)) {
                stack.pop();
                s.append(")");
            } else {
                visited.add(t);
                s.append("(" + t.val);
                if (t.left == null && t.right != null)
                    s.append("()");
                if (t.right != null)
                    stack.push(t.right);
                if (t.left != null)
                    stack.push(t.left);
            }
        }
        return s.substring(1, s.length() - 1);
    }
}

```

