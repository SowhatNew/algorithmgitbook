---
description: Medium
---

# 141 Linked List Cycle

```text
Given head, the head of a linked list, 
determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. 
Internally, pos is used to denote the index of the node that tail's next pointer is connected to. Note that pos is not passed as a parameter.

Return true if there is a cycle in the linked list. 
Otherwise, return false.

Constraints:
The number of the nodes in the list is in the range [0, 104].
-105 <= Node.val <= 105
pos is -1 or a valid index in the linked-list.
```

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Linked List Cycle.
    Memory Usage: 39.1 MB, less than 54.50% of Java online submissions for Linked List Cycle.
     */
    public boolean hasCycle(ListNode head) {
        if (head == null) {return false;}
        ListNode slow, fast;
        slow = fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) {
                return true;
            }
        }
        return false;
    }
}
```

