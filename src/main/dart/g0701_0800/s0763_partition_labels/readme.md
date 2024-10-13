[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 763\. Partition Labels

Medium

You are given a string `s`. We want to partition the string into as many parts as possible so that each letter appears in at most one part.

Note that the partition is done so that after concatenating all the parts in order, the resultant string should be `s`.

Return _a list of integers representing the size of these parts_.

**Example 1:**

**Input:** s = "ababcbacadefegdehijhklij"

**Output:** [9,7,8]

**Explanation:** The partition is "ababcbaca", "defegde", "hijhklij". This is a partition so that each letter appears in at most one part. A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits s into less parts.

**Example 2:**

**Input:** s = "eccbbbbdec"

**Output:** [10]

**Constraints:**

*   `1 <= s.length <= 500`
*   `s` consists of lowercase English letters.

## Solution

```dart
class Solution {
  List<int> partitionLabels(String s) {
    List<int> result = [];
    List<int> position = List.filled(26, 0);

    // Store the last position of each letter in the string
    for (int i = 0; i < s.length; i++) {
      position[s.codeUnitAt(i) - 'a'.codeUnitAt(0)] = i;
    }

    int i = 0;
    int prev = -1;
    int max = 0;

    while (i < s.length) {
      max = max > position[s.codeUnitAt(i) - 'a'.codeUnitAt(0)] ? max : position[s.codeUnitAt(i) - 'a'.codeUnitAt(0)];

      if (i == max) {
        result.add(i - prev);
        prev = i;
      }

      i++;
    }

    return result;
  }
}
```