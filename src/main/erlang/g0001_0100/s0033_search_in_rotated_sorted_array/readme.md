[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 33\. Search in Rotated Sorted Array

Medium

There is an integer array `nums` sorted in ascending order (with **distinct** values).

Prior to being passed to your function, `nums` is **possibly rotated** at an unknown pivot index `k` (`1 <= k < nums.length`) such that the resulting array is `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]` (**0-indexed**). For example, `[0,1,2,4,5,6,7]` might be rotated at pivot index `3` and become `[4,5,6,7,0,1,2]`.

Given the array `nums` **after** the possible rotation and an integer `target`, return _the index of_ `target` _if it is in_ `nums`_, or_ `-1` _if it is not in_ `nums`.

You must write an algorithm with `O(log n)` runtime complexity.

**Example 1:**

**Input:** nums = [4,5,6,7,0,1,2], target = 0

**Output:** 4

**Example 2:**

**Input:** nums = [4,5,6,7,0,1,2], target = 3

**Output:** -1

**Example 3:**

**Input:** nums = [1], target = 0

**Output:** -1

**Constraints:**

*   `1 <= nums.length <= 5000`
*   <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>
*   All values of `nums` are **unique**.
*   `nums` is an ascending array that is possibly rotated.
*   <code>-10<sup>4</sup> <= target <= 10<sup>4</sup></code>

## Solution

```erlang
-spec search(Nums :: [integer()], Target :: integer()) -> integer().

search(Nums, Target) ->
    search(Nums, Target, 0, length(Nums) - 1).

search(_, _, L, R) when L > R -> -1;
search(Nums, Target, L, R) ->
    Mid = (L + R) div 2,
    Val = lists:nth(Mid + 1, Nums),
    Start = lists:nth(L + 1, Nums),
    case Val of
        Target -> Mid;
        _ -> 
            if 
                (Val >= Start andalso Target >= Start andalso Target < Val) 
                orelse (Val < Start andalso (Target >= Start orelse Target < Val)) ->
                    search(Nums, Target, L, Mid - 1);
                true ->
                    search(Nums, Target, Mid + 1, R)
            end
    end.
```