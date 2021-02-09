---
description: Medium
---

# 19 Remove Nth Node From End of List

```text
Given the head of a linked list, remove the nth node from the end of the list and return its head.

Follow up: Could you do this in one pass?

Constraints:
The number of nodes in the list is sz.
1 <= sz <= 30
0 <= Node.val <= 100
1 <= n <= sz
```

## A

```text
public  class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Remove Nth Node From End of List.
    Memory Usage: 37 MB, less than 47.92% of Java online submissions for Remove Nth Node From End of List.
     */
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode root = new ListNode();
        root.next = head;

        ListNode fast, slow;
        slow = root;
        fast = root;
        for (int i = 0; i < n; i++) {
            fast = fast.next;
        }

        while (fast.next != null) {
            fast = fast.next;
            slow = slow.next;
        }
        slow.next = slow.next.next;
        
        return root.next;
    }    
}
```

## B

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Remove Nth Node From End of List.
    Memory Usage: 37 MB, less than 47.92% of Java online submissions for Remove Nth Node From End of List.
     */
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode fast = head, slow = head;
        while (fast != null) {
            if (n-- < 0) {
                slow = slow.next;
            }
            fast = fast.next;
        }
        if (n < 0) {
            slow.next = slow.next.next;
        } else {
            head = head.next;
        }
        return head;
    }
}
```

