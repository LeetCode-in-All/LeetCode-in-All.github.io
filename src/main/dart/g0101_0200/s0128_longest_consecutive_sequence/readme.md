[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 128\. Longest Consecutive Sequence

Medium

Given an unsorted array of integers `nums`, return _the length of the longest consecutive elements sequence._

You must write an algorithm that runs in `O(n)` time.

**Example 1:**

**Input:** nums = [100,4,200,1,3,2]

**Output:** 4

**Explanation:** The longest consecutive elements sequence is `[1, 2, 3, 4]`. Therefore its length is 4.

**Example 2:**

**Input:** nums = [0,3,7,2,5,8,4,6,0,1]

**Output:** 9

**Constraints:**

*   <code>0 <= nums.length <= 10<sup>5</sup></code>
*   <code>-10<sup>9</sup> <= nums[i] <= 10<sup>9</sup></code>

## Solution

```dart
class Solution {
  int longestConsecutive(List<int> nums) {
    if (nums.isEmpty) {
      return 0;
    }

    nums.sort(); // Sort the list
    int max = -999999999; // Equivalent to Integer.MIN_VALUE in Java
    int currentMax = 1;

    for (int i = 0; i < nums.length - 1; i++) {
      if (nums[i + 1] == nums[i] + 1) {
        currentMax += 1;
        continue;
      }
      if (nums[i + 1] == nums[i]) {
        continue;
      }
      // Start of a new sequence
      max = maxVal(max, currentMax);
      currentMax = 1;
    }

    return maxVal(max, currentMax);
  }

  int maxVal(int a, int b) => a > b ? a : b; // Utility function for max
}
```