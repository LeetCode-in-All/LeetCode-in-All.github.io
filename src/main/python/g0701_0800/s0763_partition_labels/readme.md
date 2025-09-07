[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 763\. Partition Labels

Medium

You are given a string `s`. We want to partition the string into as many parts as possible so that each letter appears in at most one part.

Return _a list of integers representing the size of these parts_.

**Example 1:**

**Input:** s = "ababcbacadefegdehijhklij"

**Output:** [9,7,8]

**Explanation:**

    The partition is "ababcbaca", "defegde", "hijhklij".
    This is a partition so that each letter appears in at most one part.
    A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits s into less parts. 

**Example 2:**

**Input:** s = "eccbbbbdec"

**Output:** [10] 

**Constraints:**

*   `1 <= s.length <= 500`
*   `s` consists of lowercase English letters.

## Solution

```python
from typing import List

class Solution:
    def partitionLabels(self, s: str) -> List[int]:
        letters = list(s)
        result = []
        position = [0] * 26

        for i in range(len(letters)):
            position[ord(letters[i]) - ord('a')] = i

        i = 0
        prev = -1
        max_pos = 0

        while i < len(letters):
            if position[ord(letters[i]) - ord('a')] > max_pos:
                max_pos = position[ord(letters[i]) - ord('a')]
            if i == max_pos:
                result.append(i - prev)
                prev = i
            i += 1

        return result
```