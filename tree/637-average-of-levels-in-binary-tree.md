---
description: Easy
---

# 637	Average of Levels in Binary Tree

```text
//Given a non-empty binary tree, return the average value of the nodes on each level in the form of an array.
//The range of node's value is in the range of 32-bit signed integer.
//BFS or DFS
```

## A

```text
class Solution {
    public List<Double> averageOfLevels(TreeNode root) {
        //Data type: int-->double
        //BFS
        //Queue for TreeNode, ArrayList for result.
        List<Double> result = new ArrayList<>();
        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);
        while(!q.isEmpty()){
            int n = q.size();
            double sum = 0;
            int count = 0;
            for(int i=0; i<n; i++){
                TreeNode temp = q.poll();
                sum += temp.val;
                count++;
                if(temp.left != null) q.add(temp.left);
                if(temp.right != null) q.add(temp.right);
            }
            result.add(sum/(double)count);
        }
        return result;
    }
}
```

## B

```text
class Solution {
    //Data type: int-->double
    //DFS  
    //new class Sum
    //ArrayList
    class Sum{
        double sum;
        int size;
        public Sum(int sum, int size){
            this.sum = sum;
            this.size = size;
        }
    }

    List<Sum> list = new ArrayList<>();
    public List<Double> averageOfLevels(TreeNode root){
        helper(root, 0);
        List<Double> l = new ArrayList<>();
        for(Sum s: list){
            l.add(s.sum / s.size);
        }
        return l;
    }

    private void helper(TreeNode node, int level){
        if(node == null){return;}
        if(list.size() == level){
            list.add(new Sum(node.val, 1));
        }else{
            Sum s = list.get(level);
            s.sum += node.val;
            s.size++;
        }
        helper(node.left, level+1);
        helper(node.right, level+1);
    }
}
```

