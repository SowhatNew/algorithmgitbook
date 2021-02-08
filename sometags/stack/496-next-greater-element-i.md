---
description: Easy
---

# 496 Next Greater Element I

```text
You are given two integer arrays nums1 and nums2 both of unique elements, where nums1 is a subset of nums2.

Find all the next greater numbers for nums1's elements in the corresponding places of nums2.

The Next Greater Number of a number x in nums1 is the first greater number to its right in nums2. 
If it does not exist, return -1 for this number.

 

Example 1:
Input: nums1 = [4,1,2], nums2 = [1,3,4,2]
Output: [-1,3,-1]
Explanation:
For number 4 in the first array, you cannot find the next greater number for it in the second array, so output -1.
For number 1 in the first array, the next greater number for it in the second array is 3.
For number 2 in the first array, there is no next greater number for it in the second array, so output -1.

Example 2:
Input: nums1 = [2,4], nums2 = [1,2,3,4]
Output: [3,-1]
Explanation:
For number 2 in the first array, the next greater number for it in the second array is 3.
For number 4 in the first array, there is no next greater number for it in the second array, so output -1.
 

Constraints:
1 <= nums1.length <= nums2.length <= 1000
0 <= nums1[i], nums2[i] <= 104
All integers in nums1 and nums2 are unique.
All the integers of nums1 also appear in nums2.
 

Follow up: Could you find an O(nums1.length + nums2.length) solution?
```

## A

```java
public class Solution {
    /*
    Runtime: 3 ms, faster than 83.57% of Java online submissions for Next Greater Element I.
    Memory Usage: 39 MB, less than 77.32% of Java online submissions for Next Greater Element I.
     */
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        int[] res = new int[nums1.length];
        Map<Integer, Integer> map = new HashMap<>();
        Deque<Integer> stack = new ArrayDeque<>();

        for (int num : nums2) {
            while (!stack.isEmpty() && stack.peek() <= num) {
                map.put(stack.pop(), num);
            }
            stack.push(num);
        }

        int i = 0;
        for (int num : nums1) {
            res[i++] = map.getOrDefault(num, -1);
        }

        return res;
    }
}
```

## B

```java
public class Solution {
    /*
    Runtime: 3 ms, faster than 83.57% of Java online submissions for Next Greater Element I.
    Memory Usage: 39.5 MB, less than 31.36% of Java online submissions for Next Greater Element I.
     */
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        int[] res = new int[nums1.length];
        Map<Integer, Integer> map = new HashMap<>();
        Deque<Integer> stack = new ArrayDeque<>();

        for (int i = nums2.length - 1; i >= 0; i--) {
            while (!stack.isEmpty() && stack.peek() <= nums2[i]) {
                stack.pop();
            }
            if (!stack.isEmpty()) {
                map.put(nums2[i], stack.peek());
            }
            stack.push(nums2[i]);
        }

        int i = 0;
        for (int num : nums1) {
            res[i++] = map.getOrDefault(num, -1);
        }

        return res;
    }
```

