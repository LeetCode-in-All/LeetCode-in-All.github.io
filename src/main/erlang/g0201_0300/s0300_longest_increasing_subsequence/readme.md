[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 300\. Longest Increasing Subsequence

Medium

Given an integer array `nums`, return the length of the longest strictly increasing subsequence.

A **subsequence** is a sequence that can be derived from an array by deleting some or no elements without changing the order of the remaining elements. For example, `[3,6,2,7]` is a subsequence of the array `[0,3,1,6,2,2,7]`.

**Example 1:**

**Input:** nums = [10,9,2,5,3,7,101,18]

**Output:** 4

**Explanation:** The longest increasing subsequence is [2,3,7,101], therefore the length is 4.

**Example 2:**

**Input:** nums = [0,1,0,3,2,3]

**Output:** 4

**Example 3:**

**Input:** nums = [7,7,7,7,7,7,7]

**Output:** 1

**Constraints:**

*   `1 <= nums.length <= 2500`
*   <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>

**Follow up:** Can you come up with an algorithm that runs in `O(n log(n))` time complexity?

## Solution

```erlang
-spec length_of_lis(Nums :: [integer()]) -> integer().
length_of_lis(Nums) ->
    Pred = fun(V, Index) -> { {Index, V}, Index + 1} end,
    {IVals, _} = lists:mapfoldl(Pred, 0, Nums),
    [H|T] = IVals,
    Tid = ets:new(lis, []),
    length_of_lis([], T, H, Tid, 0).

length_of_lis(Before, [], {_, Val}, Tid, Max) ->
    max(lis(Before, Val, Tid) + 1, Max);
length_of_lis(Before, [Next|After], Current={Index, Val}, Tid, Max) ->
    Lis = lis(Before, Val, Tid) + 1,
    ets:insert(Tid, {Index, Lis}),
    length_of_lis([Current|Before], After, Next, Tid, max(Max, Lis)).

lis([], _, _) -> 0;
lis(L, N, Tid) ->
    Opts = lists:filter(fun({I, V}) -> V < N end, L),
    Pred = fun({I, _}) -> ets:lookup_element(Tid, I, 2) end,
    case Opts of
        [] -> 0;
        _ ->
            lists:max(lists:map(Pred, Opts))
    end.
```