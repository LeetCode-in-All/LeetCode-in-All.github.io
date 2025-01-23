[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 239\. Sliding Window Maximum

Hard

You are given an array of integers `nums`, there is a sliding window of size `k` which is moving from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position.

Return _the max sliding window_.

**Example 1:**

**Input:** nums = [1,3,-1,-3,5,3,6,7], k = 3

**Output:** [3,3,5,5,6,7]

**Explanation:** 

Window position Max 

--------------- ----- 

[1 3 -1] -3 5 3 6 7 **3** 

1 [3 -1 -3] 5 3 6 7 **3** 

1 3 [-1 -3 5] 3 6 7 **5** 

1 3 -1 [-3 5 3] 6 7 **5** 

1 3 -1 -3 [5 3 6] 7 **6** 

1 3 -1 -3 5 [3 6 7] **7**

**Example 2:**

**Input:** nums = [1], k = 1

**Output:** [1]

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>5</sup></code>
*   <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>
*   `1 <= k <= nums.length`

## Solution

```erlang
-spec max_sliding_window(Nums :: [integer()], K :: integer()) -> [integer()].
max_sliding_window(Nums, K) ->
    {Results, _} = lists:mapfoldl(
        fun({X, I}, Q) ->
            Q2 = enqueue(Q, X, I),
            get_max(Q2, I - K)
        end,
        queue:new(),
        lists:zip(Nums, lists:seq(0, length(Nums)-1))
    ),
    lists:nthtail(K-1, Results).

-spec enqueue(queue:queue(), integer(), integer()) -> queue:queue().
enqueue(Q, X, I) ->
    case queue:peek_r(Q) of
        {value, {Y, _}} when Y =< X ->
            enqueue(queue:drop_r(Q), X, I);
        _ ->
            queue:in({X, I}, Q)
    end.

-spec get_max(queue:queue(), integer()) -> {integer(), queue:queue()}.
get_max(Q, DropUntil) ->
    case queue:peek(Q) of
        {value, {_, J}} when J =< DropUntil ->
            get_max(queue:drop(Q), DropUntil);
        {value, {Y, _}} ->
            {Y, Q}
    end.
```