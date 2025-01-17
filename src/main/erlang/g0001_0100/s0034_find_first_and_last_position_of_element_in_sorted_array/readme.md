[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 34\. Find First and Last Position of Element in Sorted Array

Medium

Given an array of integers `nums` sorted in non-decreasing order, find the starting and ending position of a given `target` value.

If `target` is not found in the array, return `[-1, -1]`.

You must write an algorithm with `O(log n)` runtime complexity.

**Example 1:**

**Input:** nums = [5,7,7,8,8,10], target = 8

**Output:** [3,4]

**Example 2:**

**Input:** nums = [5,7,7,8,8,10], target = 6

**Output:** [-1,-1]

**Example 3:**

**Input:** nums = [], target = 0

**Output:** [-1,-1]

**Constraints:**

*   <code>0 <= nums.length <= 10<sup>5</sup></code>
*   <code>-10<sup>9</sup> <= nums[i] <= 10<sup>9</sup></code>
*   `nums` is a non-decreasing array.
*   <code>-10<sup>9</sup> <= target <= 10<sup>9</sup></code>

## Solution

```erlang
-spec search_range(Nums :: [integer()], Target :: integer()) -> [integer()].
search_range(Nums, Target) ->
    [helper(Nums, Target, false), helper(Nums, Target, true)].

-spec helper(Nums :: [integer()], Target :: integer(), Equals :: boolean()) -> integer().
helper(Nums, Target, Equals) ->
    helper(Nums, Target, Equals, 0, length(Nums) - 1, -1).

-spec helper(Nums :: [integer()], Target :: integer(), Equals :: boolean(), L :: integer(), R :: integer(), Result :: integer()) -> integer().
helper(_, _, _, L, R, Result) when L > R ->
    Result;
helper(Nums, Target, Equals, L, R, Result) ->
    Mid = L + (R - L) div 2,
    MidValue = lists:nth(Mid + 1, Nums), % Erlang lists are 1-based
    NewResult = 
        case MidValue == Target of
            true -> Mid;
            false -> Result
        end,
    case MidValue < Target orelse (MidValue == Target andalso Equals) of
        true -> helper(Nums, Target, Equals, Mid + 1, R, NewResult);
        false -> helper(Nums, Target, Equals, L, Mid - 1, NewResult)
    end.
```