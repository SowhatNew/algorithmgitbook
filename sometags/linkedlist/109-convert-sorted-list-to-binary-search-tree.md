---
description: Medium
---

# 109 Convert Sorted List to Binary Search Tree

```text
Given the head of a singly linked list where elements are sorted 
in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree 
in which the depth of the two subtrees of every node never differ by more than 1.


Example 1:
Input: head = [-10,-3,0,5,9]
Output: [0,-3,9,-10,null,5]
Explanation: One possible answer is [0,-3,9,-10,null,5], which represents the shown height balanced BST.

Example 2:
Input: head = []
Output: []

Example 3:
Input: head = [0]
Output: [0]

Example 4:
Input: head = [1,3]
Output: [3,1]
 

Constraints:
The number of nodes in head is in the range [0, 2 * 104].
-10^5 <= Node.val <= 10^5
```

## A

```java
public class Solution {
    /**
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Convert Sorted List to Binary Search Tree.
	Memory Usage: 40 MB, less than 60.43% of Java online submissions for Convert Sorted List to Binary Search Tree.
    */
    public TreeNode sortedListToBST(ListNode head) {
        return buildTree(head);
    }

    // time O(N/2)*O(N) = O(N^2)
    // espace O(logN)*O(1) = O(logN)
    TreeNode buildTree(ListNode node) {
        if (node == null) {
            return null;
        }
        if (node.next == null) {
            return new TreeNode(node.val);
        }
        ListNode mid = findMiddleNode(node);
        TreeNode root = new TreeNode(mid.val);
        root.left = buildTree(node);
        root.right = buildTree(mid.next);
        return root;
    }

    // time O(N/2) = O(N)
    // espace O(1)
    ListNode findMiddleNode(ListNode head) {
        ListNode fast = head, slow = head, pre = null;
        while (fast != null && fast.next != null) {
            pre = slow;
            slow = slow.next;
            fast = fast.next.next;
        }
        pre.next = null;
        return slow;
    }
}
```

## B

```java
public class Solution {
    /**
    Runtime: 1 ms, faster than 34.36% of Java online submissions for Convert Sorted List to Binary Search Tree.
	Memory Usage: 40.2 MB, less than 39.08% of Java online submissions for Convert Sorted List to Binary Search Tree.
	 */
    public TreeNode sortedListToBST(ListNode head) {
        List<Integer>nums=new ArrayList<>();
        while(head!=null) {
            nums.add(head.val);
            head=head.next;
        }
        return BST(nums,0,nums.size()-1);
    }
    public TreeNode BST(List<Integer>nums,int low,int high) {
        if(low>high)return null;
        int mid=(low+high)/2;
        TreeNode root=new TreeNode(nums.get(mid));
        root.left=BST(nums,low,mid-1);
        root.right=BST(nums,mid+1,high);
        return root;
    }
}
```

