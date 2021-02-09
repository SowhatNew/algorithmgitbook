---
description: Easy
---

# 206 Reverse Linked List

```text
Reverse a singly linked list.

Example:

Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
Follow up:

A linked list can be reversed either iteratively or recursively. 
Could you implement both?
```

## A1

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Reverse Linked List.
    Memory Usage: 38.7 MB, less than 67.55% of Java online submissions for Reverse Linked List.
     */
    public ListNode reverseList(ListNode head) {
        if (head == null) {
            return null;
        }
        ListNode preNode, curNode, nextNode;
        preNode = null;
        curNode = head;
        nextNode = curNode.next;
        while (nextNode != null) {
            curNode.next = preNode;
            preNode = curNode;
            curNode = nextNode;
            nextNode = nextNode.next;
        }
        curNode.next = preNode;
        return curNode;
    }
}
```

## A2

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Reverse Linked List.
    Memory Usage: 38.5 MB, less than 93.87% of Java online submissions for Reverse Linked List.
     */
    public ListNode reverseList(ListNode head) {
        ListNode pre = null;
        while (head != null) {
            ListNode next = head.next;
            head.next = pre;
            pre = head;
            head = next;
        }
        return pre;
    }
}
```

## B1

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Reverse Linked List.
    Memory Usage: 38.8 MB, less than 65.14% of Java online submissions for Reverse Linked List.
     */
    public ListNode reverseList(ListNode head) {
        return helper(null, head);
    }
    private ListNode helper(ListNode pre, ListNode cur) {
        if (cur == null) {return pre;}
        ListNode next = cur.next;
        cur.next = pre;
        return helper(cur, next);
    }
}
```

## B2

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Reverse Linked List.
    Memory Usage: 38.6 MB, less than 78.99% of Java online submissions for Reverse Linked List.
     */
    public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode last = reverseList(head.next);
        head.next.next = head;
        head.next = null;
        return last;
    }
}
```

