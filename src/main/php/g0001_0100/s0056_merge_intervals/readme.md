[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 56\. Merge Intervals

Medium

Given an array of `intervals` where <code>intervals[i] = [start<sub>i</sub>, end<sub>i</sub>]</code>, merge all overlapping intervals, and return _an array of the non-overlapping intervals that cover all the intervals in the input_.

**Example 1:**

**Input:** intervals = \[\[1,3],[2,6],[8,10],[15,18]]

**Output:** [[1,6],[8,10],[15,18]]

**Explanation:** Since intervals [1,3] and [2,6] overlaps, merge them into [1,6]. 

**Example 2:**

**Input:** intervals = \[\[1,4],[4,5]]

**Output:** [[1,5]]

**Explanation:** Intervals [1,4] and [4,5] are considered overlapping. 

**Constraints:**

*   <code>1 <= intervals.length <= 10<sup>4</sup></code>
*   `intervals[i].length == 2`
*   <code>0 <= start<sub>i</sub> <= end<sub>i</sub> <= 10<sup>4</sup></code>

## Solution

```php
class Solution {
    /**
     * @param Integer[][] $intervals
     * @return Integer[][]
     */
    public function merge($intervals) {
        array_multisort($intervals);
        $res = [$intervals[0]];
        $k = 0;
        for ($i = 1; $i < count($intervals); $i++) {
            $start = $intervals[$i][0];
            $end = $intervals[$i][1];
            $last_interv = end($res);
            if ($start <= $last_interv[1]) {
                $res[$k] = [$last_interv[0], max($end, $last_interv[1])];
            } else {
                $res[] = $intervals[$i];
                $k++;
            }
        }
        return $res;
    }
}
```