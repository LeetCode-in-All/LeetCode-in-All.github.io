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

## Solution

```erlang
-spec num_trees(N :: integer()) -> integer().
num_trees(N) ->
    Result = calculate_num_trees(N, 0, 1),
    Result div (N + 1).

-spec calculate_num_trees(N :: integer(), I :: integer(), Acc :: integer()) -> integer().
calculate_num_trees(N, I, Acc) when I >= N ->
    Acc;
calculate_num_trees(N, I, Acc) ->
    calculate_num_trees(
        N,
        I + 1,
        (Acc * (2 * N - I)) div (I + 1)
    ).
```