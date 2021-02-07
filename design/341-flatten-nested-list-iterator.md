---
description: Medium
---

# 341 Flatten Nested List Iterator

```text
Given a nested list of integers, implement an iterator to flatten it.

Each element is either an integer, or a list -- whose elements may also be integers or other lists.

Example 1:

Input: [[1,1],2,[1,1]]
Output: [1,1,2,1,1]
Explanation: By calling next repeatedly until hasNext returns false, 
             the order of elements returned by next should be: [1,1,2,1,1].
Example 2:

Input: [1,[4,[6]]]
Output: [1,4,6]
Explanation: By calling next repeatedly until hasNext returns false, 
             the order of elements returned by next should be: [1,4,6].
```

## A

```text
public class NestedIterator implements Iterator<Integer> {
    /*
    Runtime: 3 ms, faster than 54.65% of Java online submissions for Flatten Nested List Iterator.
    Memory Usage: 41.1 MB, less than 93.94% of Java online submissions for Flatten Nested List Iterator.
    */
    Deque<NestedInteger> stack = new ArrayDeque<>();
    
    public NestedIterator(List<NestedInteger> nestedList) {
        prepareStack(nestedList);
    }

    @Override
    public Integer next() {
        if (!hasNext()) {
            return null;
        }
        return stack.pop().getInteger();
    }

    @Override
    public boolean hasNext() {
        while (!stack.isEmpty() && !stack.peek().isInteger()) {
            List<NestedInteger> list = stack.pop().getList();
            prepareStack(list);
        }
        return !stack.isEmpty();
    }
    
    private void prepareStack(List<NestedInteger> nestedList) {
        for (int i = nestedList.size() - 1; i >= 0; i--) {
            stack.push(nestedList.get(i));
        }
    }
}
```

## B

```text
public class NestedIterator implements Iterator<Integer> {
    /*
    Runtime: 2 ms, faster than 98.44% of Java online submissions for Flatten Nested List Iterator.
    Memory Usage: 41.2 MB, less than 83.31% of Java online submissions for Flatten Nested List Iterator.
    */
    private LinkedList<NestedInteger> list;
    
    public NestedIterator(List<NestedInteger> nestedList) {
        list = new LinkedList<>(nestedList);
    }

    @Override
    public Integer next() {
        return list.remove(0).getInteger();
    }

    @Override
    public boolean hasNext() {
        while (!list.isEmpty() && !list.get(0).isInteger()) {
            List<NestedInteger> temp = list.remove(0).getList();
            for (int i = temp.size()-1; i >= 0; i--) {
                list.addFirst(temp.get(i));
            }
        }
        return !list.isEmpty();
    }
}

```

