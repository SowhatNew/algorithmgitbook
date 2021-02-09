---
description: Medium
---

# 92 Reverse Linked List II

```text
Reverse a linked list from position m to n. Do it in one-pass.

Note: 1 ≤ m ≤ n ≤ length of list.

Example:
Input: 1->2->3->4->5->NULL, m = 2, n = 4
Output: 1->4->3->2->5->NULL
```

## A

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Reverse Linked List II.
    Memory Usage: 36.7 MB, less than 53.60% of Java online submissions for Reverse Linked List II.
     */
    public ListNode reverseBetween(ListNode head, int m, int n) {
        if (m == n) {
            return head;
        }
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        int count = 0;
        ListNode leftLeft = null;
        ListNode leftRight = null;
        ListNode pre = dummy;
        while (head != null) {
            count++;
            if (count == m) {
                leftLeft = pre;
                leftRight = head;
            } else if (count > m && count < n) {
                ListNode temp = head.next;
                head.next = pre;
                pre = head;
                head = temp;
                continue;
            } else if (count == n) {
                leftRight.next = head.next;
                head.next = pre;
                leftLeft.next = head;
                break;
            }
            head = head.next;
            pre = pre.next;
        }
        return dummy.next;
    }
}
```

## B

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Reverse Linked List II.
    Memory Usage: 36.4 MB, less than 90.68% of Java online submissions for Reverse Linked List II.
     */
    private ListNode successor;
    public ListNode reverseN(ListNode head, final int n) {
        if (n == 1) {
            successor = head.next;
            return head;
        }
        ListNode last = reverseN(head.next, n-1);
        head.next.next = head;
        head.next = successor;
        return last;
    }

    public ListNode reverseBetween(ListNode head, final int m, final int n) {
        if (m == 1) {
            return reverseN(head, n);
        }
        head.next = reverseBetween(head.next, m-1, n-1);
        return head;
    }
}
```

