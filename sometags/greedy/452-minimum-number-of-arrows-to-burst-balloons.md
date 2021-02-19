---
description: Medium
---

# 452 Minimum Number of Arrows to Burst Balloons

```text
There are some spherical balloons spread in two-dimensional space. 
For each balloon, provided input is the start and end coordinates of the horizontal diameter. 
Since it's horizontal, y-coordinates don't matter, and hence the x-coordinates of start and end of the diameter suffice. 
The start is always smaller than the end.

An arrow can be shot up exactly vertically from different points along the x-axis. 
A balloon with xstart and xend bursts by an arrow shot at x if xstart ≤ x ≤ xend. 
There is no limit to the number of arrows that can be shot. 
An arrow once shot keeps traveling up infinitely.

Given an array points where points[i] = [xstart, xend], 
return the minimum number of arrows that must be shot to burst all balloons.

 

Example 1:
Input: points = [[10,16],[2,8],[1,6],[7,12]]
Output: 2
Explanation: One way is to shoot one arrow for example 
at x = 6 (bursting the balloons [2,8] and [1,6]) and another arrow at x = 11 (bursting the other two balloons).

Example 2:
Input: points = [[1,2],[3,4],[5,6],[7,8]]
Output: 4

Example 3:
Input: points = [[1,2],[2,3],[3,4],[4,5]]
Output: 2

Example 4:
Input: points = [[1,2]]
Output: 1

Example 5:
Input: points = [[2,3],[2,3]]
Output: 1
 

Constraints:
0 <= points.length <= 104
points[i].length == 2
-231 <= xstart < xend <= 231 - 1
```

```java
class Solution {
    /*
    Runtime: 14 ms, faster than 99.59% of Java online submissions for Minimum Number of Arrows to Burst Balloons.
    Memory Usage: 46.8 MB, less than 53.19% of Java online submissions for Minimum Number of Arrows to Burst Balloons.    
     */
    public int findMinArrowShots(int[][] points) {
        if (points.length == 0) {
            return 0;
        }
        Arrays.sort(points, new Comparator<int[]>() {
            @Override
            public int compare(int[] o1, int[] o2) {
                long res = (long)o1[1] - (long)o2[1];
                if (res < 0) {
                    return -1;
                }
                if (res > 0) {
                    return 1;
                }
                return 0;
            }
        });
        int count = 1;
        int x_end = points[0][1];
        for (int i = 1; i < points.length; i++) {
            int start = points[i][0];
            if (start > x_end) {
                count++;
                x_end = points[i][1];
            }
        }
        return count;
    }
}
```

