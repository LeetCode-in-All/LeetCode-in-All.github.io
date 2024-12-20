[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 56\. Merge Intervals

Medium

Given an array of `intervals` where <code>intervals[i] = [start<sub>i</sub>, end<sub>i</sub>]</code>, merge all overlapping intervals, and return _an array of the non-overlapping intervals that cover all the intervals in the input_.

**Example 1:**

**Input:** intervals = \[\[1,3],[2,6],[8,10],[15,18]]

**Output:** [[1,6],[8,10],[15,18]]

**Explanation:** Since intervals [1,3] and [2,6] overlap, merge them into [1,6].

**Example 2:**

**Input:** intervals = \[\[1,4],[4,5]]

**Output:** [[1,5]]

**Explanation:** Intervals [1,4] and [4,5] are considered overlapping.

**Constraints:**

*   <code>1 <= intervals.length <= 10<sup>4</sup></code>
*   `intervals[i].length == 2`
*   <code>0 <= start<sub>i</sub> <= end<sub>i</sub> <= 10<sup>4</sup></code>

## Solution

```dart
class Solution {
  List<List<int>> merge(List<List<int>> intervals) {
    // Sort the intervals based on the start time
    intervals.sort((a, b) =>a[0].compareTo(b[0]));

    List<List<int>> merged = [];
    List<int> current = intervals[0];
    merged.add(current);

    for (List<int> next in intervals){
      if (current[1] >= next[0]) {
        // If the intervals overlap, merge them
        current[1] = current[1] > next[1] ? current[1] : next[1];
      } else {
        // Otherwise, move to the next interval
        current = next;
        merged.add(current);
      }
    }

    return merged;
  }
}
```