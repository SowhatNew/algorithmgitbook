---
description: Medium
---

# 142 Linked List Cycle II

```text
Given a linked list, return the node where the cycle begins. 
If there is no cycle, return null.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. 
Internally, pos is used to denote the index of the node that tail's next pointer is connected to. 
Note that pos is not passed as a parameter.

Notice that you should not modify the linked list.

Constraints:
The number of the nodes in the list is in the range [0, 104].
-105 <= Node.val <= 105
pos is -1 or a valid index in the linked-list.
```

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Linked List Cycle II.
    Memory Usage: 38.9 MB, less than 78.04% of Java online submissions for Linked List Cycle II.
     */
    public ListNode detectCycle(ListNode head) {
        ListNode slow, fast;
        slow = fast = head;
        boolean hasCycle = false;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) {
                hasCycle = true;
                break;
            }
        }
        if (!hasCycle) {
            return null;
        }
        slow = head;
        while (slow != fast) {
            slow = slow.next;
            fast = fast.next;
        }
        return slow;
    }
}
```

