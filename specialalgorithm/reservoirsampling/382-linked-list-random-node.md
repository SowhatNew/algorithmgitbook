---
description: Medium
---

# 382 Linked List Random Node

```text
Given a singly linked list, return a random node's value from the linked list. 
Each node must have the same probability of being chosen.

 

Example 1:

Input
["Solution", "getRandom", "getRandom", "getRandom", "getRandom", "getRandom"]
[[[1, 2, 3]], [], [], [], [], []]
Output
[null, 1, 3, 2, 2, 3]

Explanation
Solution solution = new Solution([1, 2, 3]);
solution.getRandom(); // return 1
solution.getRandom(); // return 3
solution.getRandom(); // return 2
solution.getRandom(); // return 2
solution.getRandom(); // return 3
// getRandom() should return either 1, 2, or 3 randomly. Each element should have equal probability of returning.
 

Constraints:
The number of nodes in the linked list will be in the range [1, 104]
-104 <= Node.val <= 104
At most 104 calls will be made to getRandom.
 

Follow up:
What if the linked list is extremely large and its length is unknown to you?
Could you solve this efficiently without using extra space?
```



Explain

$$
\frac{1}{i} \times\ (1 - \frac{1}{i+1}) \times\ (1 - \frac{1}{i+2}) \times\ ... \times\ (1 - \frac{1}{n}) \\
	= \frac{1}{i} \times\ \frac{i}{i+1} \times\ \frac{i+1}{i+2} \times\ ... \times\ \frac{n-1}{n}  \\
	= \frac{1}{n}
$$

```java
class Solution {
    /*
    Runtime: 15 ms, faster than 29.10% of Java online submissions for Linked List Random Node.
    Memory Usage: 41 MB, less than 47.69% of Java online submissions for Linked List Random Node.
     */
    private ListNode head;

    /** @param head The linked list's head.
        Note that the head is guaranteed to be not null, so it contains at least one node. */
    public Solution(ListNode head) {
        this.head = head;
    }
    
    /** Returns a random node's value. */
    public int getRandom() {
        Random r = new Random();
        int i = 0, res = 0;
        ListNode p = head;
        while (p != null) {
            if (r.nextInt(++i) == 0) {
                res = p.val;
            }
            p = p.next;
        }
        return res;        
    }
}
```

