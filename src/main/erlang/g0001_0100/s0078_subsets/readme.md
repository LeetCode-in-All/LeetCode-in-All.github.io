[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 78\. Subsets

Medium

Given an integer array `nums` of **unique** elements, return _all possible subsets (the power set)_.

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

**Example 1:**

**Input:** nums = [1,2,3]

**Output:** [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]

**Example 2:**

**Input:** nums = [0]

**Output:** [[],[0]]

**Constraints:**

*   `1 <= nums.length <= 10`
*   `-10 <= nums[i] <= 10`
*   All the numbers of `nums` are **unique**.

## Solution

```erlang
-spec subsets(Nums :: [integer()]) -> [[integer()]].

make(N, _, Tmp, Cnt) when Cnt =:= N -> [Tmp];
make(_, [], _, _) -> [];
make(N, [H | T], Tmp, Cnt) -> 
    make(N, T, Tmp ++ [H], Cnt + 1) ++
    make(N, T, Tmp, Cnt).

subsets(Nums) ->
    lists:foldl(
        fun(N, Ans) ->
            Ans ++ make(N, Nums, [], 0)
        end, [], lists:seq(0, length(Nums))
    ).
```