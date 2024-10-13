[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 39\. Combination Sum

Medium

Given an array of **distinct** integers `candidates` and a target integer `target`, return _a list of all **unique combinations** of_ `candidates` _where the chosen numbers sum to_ `target`_._ You may return the combinations in **any order**.

The **same** number may be chosen from `candidates` an **unlimited number of times**. Two combinations are unique if the frequency of at least one of the chosen numbers is different.

It is **guaranteed** that the number of unique combinations that sum up to `target` is less than `150` combinations for the given input.

**Example 1:**

**Input:** candidates = [2,3,6,7], target = 7

**Output:** [[2,2,3],[7]]

**Explanation:** 
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.

7 is a candidate, and 7 = 7. 

These are the only two combinations.

**Example 2:**

**Input:** candidates = [2,3,5], target = 8

**Output:** [[2,2,2,2],[2,3,3],[3,5]]

**Example 3:**

**Input:** candidates = [2], target = 1

**Output:** []

**Constraints:**

*   `1 <= candidates.length <= 30`
*   `1 <= candidates[i] <= 200`
*   All elements of `candidates` are **distinct**.
*   `1 <= target <= 500`

## Solution

```dart
class Solution {
  List<List<int>> combinationSum(List<int> coins, int amount) {
    List<List<int>> ans = [];
    List<int> subList = [];
    combinationSumRec(coins.length, coins, amount, subList, ans);
    return ans;
  }

  void combinationSumRec(int n, List<int> coins, int amount, List<int> subList, List<List<int>> ans) {
    if (amount == 0 || n == 0) {
      if (amount == 0) {
        // Create a new list from subList and add to ans
        ans.add(List.from(subList));
      }
      return;
    }

    if (amount - coins[n - 1] >= 0) {
      subList.add(coins[n - 1]);
      combinationSumRec(n, coins, amount - coins[n - 1], subList, ans);
      // Remove the last element
      subList.removeLast();
    }

    combinationSumRec(n - 1, coins, amount, subList, ans);
  }
}
```