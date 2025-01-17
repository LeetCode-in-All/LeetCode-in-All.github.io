[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 45\. Jump Game II

Medium

Given an array of non-negative integers `nums`, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

You can assume that you can always reach the last index.

**Example 1:**

**Input:** nums = [2,3,1,1,4]

**Output:** 2

**Explanation:** The minimum number of jumps to reach the last index is 2. Jump 1 step from index 0 to 1, then 3 steps to the last index.

**Example 2:**

**Input:** nums = [2,3,0,1,4]

**Output:** 2

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>4</sup></code>
*   `0 <= nums[i] <= 1000`

## Solution

```erlang
-spec jump(Nums :: [integer()]) -> integer().
jump(Nums) ->
    jump(Nums, 0, 0, 0).

% Main jump function that counts the number of jumps
-spec jump(Nums :: [integer()], L :: integer(), R :: integer(), Jumps :: integer()) -> integer().
jump(Nums, L, R, Jumps) when R < length(Nums) - 1 ->
    Prev = R,
    NewR = get_max(Nums, L, R),
    jump(Nums, Prev + 1, NewR, Jumps + 1);
jump(_, _, _, Jumps) -> 
    Jumps.

% Helper function to get the maximum reachable index within a range
-spec get_max(Nums :: [integer()], L :: integer(), R :: integer()) -> integer().
get_max(Nums, L, R) ->
    get_max(Nums, L, R, -1).

% Recursive get_max to calculate the max reachable index
get_max(Nums, L, R, Max) when L =< R ->
    Curr = L + lists:nth(L + 1, Nums),
    NewMax = max(Curr, Max),
    get_max(Nums, L + 1, R, NewMax);
get_max(_, _, _, Max) -> Max.
```