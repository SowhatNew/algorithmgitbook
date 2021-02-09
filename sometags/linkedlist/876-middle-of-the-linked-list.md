---
description: Easy
---

# 876 Middle of the Linked List

```text
Given a non-empty, singly linked list with head node head, return a middle node of linked list.

If there are two middle nodes, return the second middle node.

Note:
The number of nodes in the given list will be between 1 and 100.
```

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Middle of the Linked List.
    Memory Usage: 36.4 MB, less than 34.04% of Java online submissions for Middle of the Linked List.
     */
    public ListNode middleNode(ListNode head) {
        ListNode slow, fast;
        slow = fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast =fast.next.next;
        }
        return slow;
    }
}
```

