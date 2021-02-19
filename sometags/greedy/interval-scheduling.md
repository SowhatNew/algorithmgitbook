# Interval Scheduling

```java
class Solution {
    // 请你设计一个算法，算出这些区间中最多有几个互不相交的区间。

    public static void main(String[] args) {
        int[][] intvs = new int[][]{{1,3}, {2,4}, {3,6}};
        System.out.println(new Solution().intervalSchedule(intvs));
        return;
    }

    public int intervalSchedule(int[][] intvs) {
        if (intvs.length == 0) {
            return 0;
        }
        Arrays.sort(intvs, new Comparator<int[]>() {
            @Override
            public int compare(int[] o1, int[] o2) {
                return o1[1] - o2[1];
            }
        });
        int count = 1;
        int x_end = intvs[0][1];
        for (int[] interval : intvs) {
            int start = interval[0];
            if (start >= x_end) {
                count++;
                x_end = interval[1];
            }
        }
        return count;
    }
}
```

