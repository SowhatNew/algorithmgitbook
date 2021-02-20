---
description: Medium
---

# 46 Permutations

```text
Given an array nums of distinct integers, return all the possible permutations. You can return the answer in any order.


Example 1:
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

Example 2:
Input: nums = [0,1]
Output: [[0,1],[1,0]]

Example 3:
Input: nums = [1]
Output: [[1]]
 

Constraints:
1 <= nums.length <= 6
-10 <= nums[i] <= 10
All the integers of nums are unique.
```

## A

```java
class Solution {
    /*
    Runtime: 2 ms, faster than 52.35% of Java online submissions for Permutations.
    Memory Usage: 39.7 MB, less than 19.95% of Java online submissions for Permutations.
     */
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> res = new LinkedList<>();
        backtrack(nums, new LinkedList<>(), res);
        return res;
    }

    private void backtrack(int[] nums, LinkedList<Integer> track, List<List<Integer>> res) {
        if (track.size() == nums.length) {
            res.add(new ArrayList<>(track));
            return;
        }

        for (int i = 0; i < nums.length; i++) {
            if (track.contains(nums[i])) {
                continue;
            }
            track.add(nums[i]);
            backtrack(nums, track, res);
            track.removeLast();
        }
    }
}
```

## B

```java
class Solution {
    /*
    Runtime: 4 ms, faster than 13.71% of Java online submissions for Permutations.
    Memory Usage: 39.3 MB, less than 59.41% of Java online submissions for Permutations.
     */
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        perm(res, nums, 0, nums.length-1);
        return res;
    }

    private static void perm(List<List<Integer>> res, int[] nums, int start, int end){
        if(start == end){
            res.add(Arrays.stream(nums).boxed().collect(Collectors.toList()));
            return;
        }
        for(int i = start; i <= end; i++){
            int temp = nums[start];
            nums[start] = nums[i];
            nums[i] = temp;

            perm(res, nums,start+1, end);

            temp = nums[start];
            nums[start] = nums[i];
            nums[i] = temp;
        }
    }
}
```

