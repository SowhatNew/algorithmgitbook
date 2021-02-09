---
description: Easy
---

# 234 Palindrome Linked List

```text
Given a singly linked list, determine if it is a palindrome.

Example 1:
Input: 1->2
Output: false

Example 2:
Input: 1->2->2->1
Output: true
Follow up:
Could you do it in O(n) time and O(1) space?
```

## A

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Palindrome Linked List.
    Memory Usage: 41.6 MB, less than 79.38% of Java online submissions for Palindrome Linked List.
     */
    public boolean isPalindrome(ListNode head) {
        if(head == null) {
            return true;
        }

        ListNode fast = head;
        ListNode slowCur = head;
        ListNode slowNext = slowCur.next;
        ListNode slowPre;

        while (fast.next != null && fast.next.next != null) {
            fast = fast.next.next;
            slowPre = slowCur;
            slowCur = slowNext;
            slowNext = slowNext.next;
            slowCur.next = slowPre;
        }

        ListNode toRight = slowNext;
        ListNode toLeft = slowCur;

        // odd
        if(fast.next == null) {
            toLeft = toLeft.next;
        }

        while (toRight != null) {
            if (toLeft.val != toRight.val) {
                return false;
            }
            toLeft = toLeft.next;
            toRight = toRight.next;
        }
        return true;
    }
}
```

## B

```text
public class Solution {
    /*
    Runtime: 1 ms, faster than 95.91% of Java online submissions for Palindrome Linked List.
    Memory Usage: 42.1 MB, less than 53.86% of Java online submissions for Palindrome Linked List.
     */
    public boolean isPalindrome(ListNode head) {
        ListNode slow, fast;
        slow = fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        if (fast != null) {
            slow = slow.next;
        }
        ListNode left = head;
        ListNode right = reverse(slow);

        while (right != null) {
            if (left.val != right.val) {
                return false;
            }
            left = left.next;
            right = right.next;
        }

        return true;
    }

    private ListNode reverse(ListNode head) {
        ListNode pre = null;
        while (head != null) {
            ListNode temp = head.next;
            head.next = pre;
            pre = head;
            head = temp;
        }
        return pre;
    }
}
```

## C

```text
public class Solution {
    /*
    Runtime: 1 ms, faster than 95.91% of Java online submissions for Palindrome Linked List.
    Memory Usage: 45.6 MB, less than 9.98% of Java online submissions for Palindrome Linked List.
     */
    private ListNode node;
    public boolean isPalindrome(ListNode head) {
        node = head;
        return head == null ? true : helper(head);
    }
    private boolean helper(ListNode head) {
        boolean flag = true;
        if (head.next != null) {
            flag = helper(head.next);
        }
        if (flag && node.val == head.val) {
            node = node.next;
            return true;
        }
        return false;
    }
}
```

