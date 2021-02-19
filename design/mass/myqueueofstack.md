# MyQueueOfStack

```java
class MyQueueOfStack {
    private Deque<Integer> s1, s2;

    public MyQueueOfStack() {
        s1 = new LinkedList<>();
        s2 = new LinkedList<>();
    }

    public void offer(int x) {
        s1.push(x);
    }

    public int peek() {
        if (s2.isEmpty()) {
            while (!s1.isEmpty()) {
                s2.push(s1.pop());
            }
        }
        return s2.peek();
    }

    public int poll() {
        peek();
        return s2.pop();
    }

    public boolean isEmpty() {
        return s1.isEmpty() && s2.isEmpty();
    }
}
```

