# MyStackOfQueue

```java
class MyStackOfQueue {
    private Queue<Integer> q;
    private Integer top_elem;

    public MyStackOfQueue() {
        q = new LinkedList<>();
        top_elem = null;
    }

    public void push(int x) {
        q.offer(x);
        top_elem = x;
    }

    public int peek() {
        return top_elem;
    }

    public int pop() {
        int size = q.size();

        if (size <= 1) {
            top_elem = null;
            return q.poll();
        }

        while (size-- > 2) {
            q.offer(q.poll());
        }
        top_elem = q.peek();
        q.offer(q.poll());

        return q.poll();
    }

    public boolean isEmpty() {
        return q.isEmpty();
    }
}
```

