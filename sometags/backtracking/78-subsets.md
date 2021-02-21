---
description: Medium
---

# 78 Subsets

```text
Given an integer array nums of unique elements, return all possible subsets (the power set).

The solution set must not contain duplicate subsets. Return the solution in any order.

 

Example 1:
Input: nums = [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]

Example 2:
Input: nums = [0]
Output: [[],[0]]
 

Constraints:
1 <= nums.length <= 10
-10 <= nums[i] <= 10
All the numbers of nums are unique.
```

```java
class Solution {
    /*
    Runtime: 1 ms, faster than 64.24% of Java online submissions for Subsets.
    Memory Usage: 39.7 MB, less than 21.52% of Java online submissions for Subsets.
     */
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        backtrack(nums, 0, new ArrayList<>(nums.length), res);
        return res;
    }

    private void backtrack(final int[] nums, int start, List<Integer> track,
                           List<List<Integer>> res) {
        res.add(new ArrayList<>(track));
        for (int i = start; i < nums.length; i++) {
            track.add(nums[i]);
            backtrack(nums, i + 1, track, res);
            track.remove(track.size()-1);
        }
    }
}
```

