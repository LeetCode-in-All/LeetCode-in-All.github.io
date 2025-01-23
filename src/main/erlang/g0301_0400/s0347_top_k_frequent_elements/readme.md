[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 347\. Top K Frequent Elements

Medium

Given an integer array `nums` and an integer `k`, return _the_ `k` _most frequent elements_. You may return the answer in **any order**.

**Example 1:**

**Input:** nums = [1,1,1,2,2,3], k = 2

**Output:** [1,2]

**Example 2:**

**Input:** nums = [1], k = 1

**Output:** [1]

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>5</sup></code>
*   <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>
*   `k` is in the range `[1, the number of unique elements in the array]`.
*   It is **guaranteed** that the answer is **unique**.

**Follow up:** Your algorithm's time complexity must be better than `O(n log n)`, where n is the array's size.

## Solution

```erlang
-spec top_k_frequent(Nums :: [integer()], K :: integer()) -> [integer()].
top_k_frequent(Nums, K) ->
    % Count frequencies using a map
    FreqMap = lists:foldl(
        fun(N, Map) ->
            maps:update_with(N, fun(V) -> V + 1 end, 1, Map)
        end,
        #{},
        Nums
    ),
    
    % Convert map to list, sort by frequency (descending), take K elements
    FreqList = maps:to_list(FreqMap),
    SortedList = lists:sort(
        fun({_, Count1}, {_, Count2}) -> Count1 > Count2 end,
        FreqList
    ),
    TopK = lists:sublist(SortedList, K),
    
    % Extract only the numbers from the result
    [Num || {Num, _Count} <- TopK].
```