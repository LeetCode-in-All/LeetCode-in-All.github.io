[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 46\. Permutations

Medium

Given an array `nums` of distinct integers, return _all the possible permutations_. You can return the answer in **any order**.

**Example 1:**

**Input:** nums = [1,2,3]

**Output:** [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

**Example 2:**

**Input:** nums = [0,1]

**Output:** [[0,1],[1,0]]

**Example 3:**

**Input:** nums = [1]

**Output:** [[1]]

**Constraints:**

*   `1 <= nums.length <= 6`
*   `-10 <= nums[i] <= 10`
*   All the integers of `nums` are **unique**.

## Solution

```dart
class Solution {
  List<List<int>> permute(List<int> nums) {
    List<List<int>> ans = [];
    List<bool> used = List<bool>.filled(nums.length, false);
    helper(ans, [], used, nums);
    return ans;
  }
  
  void helper(List<List<int>> ans, List<int> temp, List<bool> used, List<int> nums) {
    if (temp.length == nums.length) {
      ans.add(List<int>.from(temp));
      return;
    }

    for (int i = 0; i < nums.length; i++) {
      if (used[i]) continue;
      temp.add(nums[i]);
      used[i] = true;
      helper(ans, temp, used, nums);
      temp.removeLast();
      used[i] = false;
    }
  }
}
```