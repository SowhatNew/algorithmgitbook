---
description: Hard
---

# 25\* Reverse Nodes in k-Group

```text
Given a linked list, reverse the nodes of a linked list k at a time and return its modified list.

k is a positive integer and is less than or equal to the length of the linked list. 
If the number of nodes is not a multiple of k then left-out nodes, 
in the end, should remain as it is.

Follow up:
Could you solve the problem in O(1) extra memory space?
You may not alter the values in the list's nodes, only nodes itself may be changed.

Input: head = [1,2,3,4,5], k = 2
Output: [2,1,4,3,5]

Input: head = [1,2,3,4,5], k = 3
Output: [3,2,1,4,5]

Constraints:
The number of nodes in the list is in the range sz.
1 <= sz <= 5000
0 <= Node.val <= 1000
1 <= k <= sz
```

## A1

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Reverse Nodes in k-Group.
    Memory Usage: 39.1 MB, less than 69.07% of Java online submissions for Reverse Nodes in k-Group.
     */
    public ListNode reverseKGroup(ListNode head, final int k) {
        if (head == null) {
            return null;
        }
        
        ListNode start, end;
        start = head;
        end = head;
        for (int i = 0; i < k; i++) {
            if (end == null) {
                return head;
            }
            end = end.next;
        }
        ListNode res =  reverse(start, end);
        start.next = reverseKGroup(end, k);
        return res;
    }
    
    // [start, end)
    private ListNode reverse(ListNode start, ListNode end) {
        ListNode preNode, curNode, nextNode;
        preNode = null;
        curNode = start;
        nextNode = start;
        while (curNode != end) {
            nextNode = curNode.next;
            curNode.next = preNode;
            preNode = curNode;
            curNode = nextNode;
        }
        return preNode;
    }
}
```

## A2

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Reverse Nodes in k-Group.
    Memory Usage: 39.4 MB, less than 45.06% of Java online submissions for Reverse Nodes in k-Group.
     */
    public ListNode reverseKGroup(ListNode head, final int k) {
        if (head == null) {
            return null;
        }

        ListNode point = head;
        int i = k;
        while (--i > 0) {
            point = point.next;
            if (point == null) {
                return head;
            }
        }
        ListNode other = point.next;
        point.next = null;

        ListNode res = reverse(head);
        head.next = reverseKGroup(other, k);
        return res;
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

## B

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Reverse Nodes in k-Group.
    Memory Usage: 39.1 MB, less than 69.07% of Java online submissions for Reverse Nodes in k-Group.
     */
    public ListNode reverseKGroup(ListNode head, final int k) {
        if (head == null) {
            return null;
        }

        ListNode dummy = new ListNode(0);
        dummy.next = head;

        ListNode curSubHead = head;
        ListNode curSubTail = head;
        ListNode preSubTail = dummy;
        while (curSubHead != null) {
            int i = k;
            while (--i > 0) {
                curSubTail = curSubTail.next;
                if (curSubTail == null) {
                    return dummy.next;
                }
            }
            ListNode nextSubHead = curSubTail.next;
            curSubTail.next = null;

            ListNode newSubHead = reverse(curSubHead);
            preSubTail.next = newSubHead;
            curSubHead.next = nextSubHead;

            preSubTail = curSubHead;
            curSubHead = nextSubHead;
            curSubTail = nextSubHead;
        }
        return dummy.next;
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
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Reverse Nodes in k-Group.
    Memory Usage: 39.1 MB, less than 69.07% of Java online submissions for Reverse Nodes in k-Group.
     */
    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode cur = head;
        int count = 0;
        while (cur != null && count != k) {
            cur = cur.next;
            count++;
        }
        if (count != k) {
            return head;
        }
        cur = reverseKGroup(cur, k);
        while (count-- > 0) {
            ListNode temp = head.next;
            head.next = cur;
            cur = head;
            head = temp;
        }
        head = cur;
        return head;
    }
}
```

## D

```text
public class Solution {
    /*
    Runtime: 0 ms, faster than 100.00% of Java online submissions for Reverse Nodes in k-Group.
    Memory Usage: 39.1 MB, less than 69.07% of Java online submissions for Reverse Nodes in k-Group.
     */
    public ListNode reverseKGroup(ListNode head, int k) {
        if (head == null || head.next == null || k == 1) {
            return head;
        }

        ListNode begin;
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        begin = dummy;
        int i = 0;
        while (head != null) {
            i++;
            if (i % k == 0) {
                begin = helper(begin, head.next);
                head = begin.next;
            } else {
                head = head.next;
            }
        }

        return dummy.next;
    }

    private ListNode helper(ListNode begin, ListNode end) {
        ListNode cur = begin.next;
        ListNode next, first, pre;
        pre = begin;
        first = cur;
        while (cur != end) {
            next = cur.next;
            cur.next = pre;
            pre = cur;
            cur = next;
        }
        begin.next = pre;
        first.next = cur;
        return first;
    }
}
```

