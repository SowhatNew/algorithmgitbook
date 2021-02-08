---
description: Hard
---

# 295\* Find Median from Data Stream

```text
Median is the middle value in an ordered integer list. 
If the size of the list is even, there is no middle value. 
So the median is the mean of the two middle value.

For example,
[2,3,4], the median is 3

[2,3], the median is (2 + 3) / 2 = 2.5

Design a data structure that supports the following two operations:

void addNum(int num) - Add a integer number from the data stream to the data structure.
double findMedian() - Return the median of all elements so far.
 

Example:
addNum(1)
addNum(2)
findMedian() -> 1.5
addNum(3) 
findMedian() -> 2
 

Follow up:

If all integer numbers from the stream are between 0 and 100, how would you optimize it?
If 99% of all integer numbers from the stream are between 0 and 100, how would you optimize it?
```

## A1

```java
class MedianFinder {
    /*
    Runtime: 50 ms, faster than 69.03% of Java online submissions for Find Median from Data Stream.
    Memory Usage: 50.5 MB, less than 58.01% of Java online submissions for Find Median from Data Stream.
     */
    private PriorityQueue<Integer> large;
    private PriorityQueue<Integer> small;
    private boolean even;

    public MedianFinder() {
        large = new PriorityQueue<>();
        small = new PriorityQueue<>(Collections.reverseOrder());
        even = true;
    }

    public double findMedian() {
        if (even) {
            return (small.peek() + large.peek()) / 2.0;
        } else {
            return small.peek();
        }
    }

    public void addNum(int num) {
        if (even) {
            large.offer(num);
            small.offer(large.poll());
        } else {
            small.offer(num);
            large.offer(small.poll());
        }
        even = !even;
    }
}
```

## A2

```java
class MedianFinder {
    /*
    Runtime: 51 ms, faster than 65.06% of Java online submissions for Find Median from Data Stream.
    Memory Usage: 50.2 MB, less than 84.88% of Java online submissions for Find Median from Data Stream.
     */
    Queue<Integer>
            q = new PriorityQueue(),
            z = q,
            t,
            Q = new PriorityQueue(Collections.reverseOrder());

    public void addNum(int num) {
        (t=Q).add(num);
        (Q=q).add((q=t).poll());
    }

    public double findMedian() {
        return (Q.peek() + z.peek()) / 2.0;
    }
}
```

## A3

```java
class MedianFinder {
    /*
    Runtime: 51 ms, faster than 65.06% of Java online submissions for Find Median from Data Stream.
    Memory Usage: 50 MB, less than 90.84% of Java online submissions for Find Median from Data Stream.
     */
    private PriorityQueue<Integer> large;
    private PriorityQueue<Integer> small;

    public MedianFinder() {
        large = new PriorityQueue<>();
        small = new PriorityQueue<>(Collections.reverseOrder());
    }

    public double findMedian() {
        if (large.size() < small.size()) {
            return small.peek();
        } else if (large.size() > small.size()) {
            return large.peek();
        }
        return (large.peek() + small.peek()) * 0.5;
    }

    public void addNum(int num) {
        if (small.size() >= large.size()) {
            small.offer(num);
            large.offer(small.poll());
        } else {
            large.offer(num);
            small.offer(large.poll());
        }
    }
}
```

