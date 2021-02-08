---
description: Medium
---

# 284 Peeking Iterator

```text
//Given an Iterator class interface with methods: next() and hasNext(),
// design and implement a PeekingIterator that support the peek() operation --
// it essentially peek() at the element that will be returned by the next call to next().
```

## A

```text
class PeekingIterator implements Iterator<Integer> {
    /*
    Runtime: 4 ms, faster than 94.14% of Java online submissions for Peeking Iterator.
    Memory Usage: 38.9 MB, less than 74.25% of Java online submissions for Peeking Iterator.
     */
    private Integer next = null;
    private Iterator<Integer> iter;
    public PeekingIterator(Iterator<Integer> iterator) {
        // initialize any member here.
        this.iter = iterator;
        if (iter.hasNext()) {
            next = iter.next();
        }
    }

    // Returns the next element in the iteration without advancing the iterator.
    public Integer peek() {
        return next;
    }

    // hasNext() and next() should behave the same as in the Iterator interface.
    // Override them if needed.
    @Override
    public Integer next() {
        Integer res = next;
        next = iter.hasNext() ? iter.next() : null;
        return res;
    }

    @Override
    public boolean hasNext() {
        return next != null;
    }
}
```

## B

```text
class PeekingIterator implements Iterator<Integer> {
    /*
    Runtime: 4 ms, faster than 94.14% of Java online submissions for Peeking Iterator.
    Memory Usage: 38.6 MB, less than 99.48% of Java online submissions for Peeking Iterator.
     */
    private Iterator<Integer> iterator;
    public PeekingIterator(Iterator<Integer> iterator) {
        // initialize any member here.
        this.iterator = iterator;
        isPeek  = false;
    }

    private boolean isPeek;
    private Integer cur;
    // Returns the next element in the iteration without advancing the iterator.
    public Integer peek() {
        if (isPeek) {
            return cur;
        }
        isPeek = true;
        cur = iterator.next();
        return cur;
    }

    // hasNext() and next() should behave the same as in the Iterator interface.
    // Override them if needed.
    @Override
    public Integer next() {
        if (isPeek) {
            isPeek = false;
            return cur;
        }
        return iterator.next();
    }

    @Override
    public boolean hasNext() {
        return iterator.hasNext() || isPeek;
    }
}
```

