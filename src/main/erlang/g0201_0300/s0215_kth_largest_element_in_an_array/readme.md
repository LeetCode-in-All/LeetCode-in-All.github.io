[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 215\. Kth Largest Element in an Array

Medium

Given an integer array `nums` and an integer `k`, return _the_ <code>k<sup>th</sup></code> _largest element in the array_.

Note that it is the <code>k<sup>th</sup></code> largest element in the sorted order, not the <code>k<sup>th</sup></code> distinct element.

You must solve it in `O(n)` time complexity.

**Example 1:**

**Input:** nums = [3,2,1,5,6,4], k = 2

**Output:** 5

**Example 2:**

**Input:** nums = [3,2,3,1,2,4,5,5,6], k = 4

**Output:** 4

**Constraints:**

*   <code>1 <= k <= nums.length <= 10<sup>5</sup></code>
*   <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>

## Solution

```erlang
-spec find_kth_largest(Nums :: [integer()], K :: integer()) -> integer().
find_kth_largest(Nums, K) ->
    Q = gb_sets:new(),
    FinalQ = lists:foldl(fun({N, I}, AccQ) ->
        case gb_sets:is_element({N, I}, AccQ) of
            true -> AccQ;
            false ->
                case gb_sets:size(AccQ) < K of
                    true ->
                        gb_sets:insert({N, I}, AccQ);
                    false ->
                        {Smallest, TempQ} = gb_sets:take_smallest(AccQ),
                        gb_sets:insert(max(Smallest, {N, I}), TempQ)
                end
        end
    end, Q, lists:zip(Nums, lists:seq(1, length(Nums)))),
    element(1, gb_sets:smallest(FinalQ)).

% Helper function to find the maximum of two tuples based on their first element.
max({N1, I1}, {N2, I2}) when N1 >= N2 -> {N1, I1};
max(_, {N2, I2}) -> {N2, I2}.
```