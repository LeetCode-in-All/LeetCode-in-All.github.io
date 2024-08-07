[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 96\. Unique Binary Search Trees

Medium

Given an integer `n`, return _the number of structurally unique **BST'**s (binary search trees) which has exactly_ `n` _nodes of unique values from_ `1` _to_ `n`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/18/uniquebstn3.jpg)

**Input:** n = 3

**Output:** 5 

**Example 2:**

**Input:** n = 1

**Output:** 1 

**Constraints:**

*   `1 <= n <= 19`

To solve the "Unique Binary Search Trees" problem in Swift with the Solution class, follow these steps:

1. Define a method `numTrees` in the `Solution` class that takes an integer `n` as input and returns the number of structurally unique BSTs (binary search trees) with exactly `n` nodes.
2. Implement a dynamic programming approach to solve the problem:
   - Create an array `dp` of size `n + 1` to store the number of unique BSTs for each number of nodes from 0 to `n`.
   - Initialize `dp[0] = 1` and `dp[1] = 1`, as there is only one unique BST for 0 and 1 node(s).
   - Use a nested loop to calculate `dp[i]` for each `i` from 2 to `n`.
   - For each `i`, calculate `dp[i]` by summing up the products of `dp[j]` and `dp[i - j - 1]` for all possible values of `j` from 0 to `i - 1`.
   - Return `dp[n]`, which represents the number of unique BSTs with `n` nodes.

Here's the implementation of the `numTrees` method in Swift:

```swift
class Solution {
    func numTrees(_ n: Int) -> Int {
        var result: Int64 = 1
        for i in 0..<n {
            result *= Int64(2 * n - i)
            result /= Int64(i + 1)
        }
        result /= Int64(n + 1)
        return Int(result)
    }
}
```

This implementation uses dynamic programming to compute the number of structurally unique BSTs with `n` nodes in O(n^2) time complexity.