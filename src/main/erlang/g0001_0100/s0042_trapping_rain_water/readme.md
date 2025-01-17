[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 42\. Trapping Rain Water

Hard

Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)

**Input:** height = [0,1,0,2,1,0,1,3,2,1,2,1]

**Output:** 6

**Explanation:** The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.

**Example 2:**

**Input:** height = [4,2,0,3,2,5]

**Output:** 9

**Constraints:**

*   `n == height.length`
*   <code>1 <= n <= 2 * 10<sup>4</sup></code>
*   <code>0 <= height[i] <= 10<sup>5</sup></code>

## Solution

```erlang
-spec trap(Height :: [integer()]) -> integer().
trap(Height) ->
    N = length(Height),
    {_Max_val, Max_idx} = max_height(Height),
    First_half = sub_array(Height, Max_idx),
    Second_half = sub_array(lists:reverse(Height), N - Max_idx - 1),
    Result = process_heights(First_half) + process_heights(Second_half),
    Result.
    %%reverse_array(Height).


process_heights(List) ->
    process_heights(List, 0, 0).

process_heights([], _Cur_max, Result) ->
    Result;
process_heights([Head | Rest], Cur_max, Cur_res) when Head > Cur_max ->
    process_heights(Rest, Head, Cur_res);
process_heights([Head | Rest], Cur_max, Cur_res) ->
    New_res = Cur_res + Cur_max - Head,
    process_heights(Rest, Cur_max, New_res).


max_height([Head | Rest]) ->
    max_height(Rest, {Head, 0}, 1).

max_height([Head | Rest], {Cur_max, _Idx}, Idx) when Head > Cur_max ->
    max_height(Rest, {Head, Idx}, Idx + 1);
max_height([_Head | Rest], Cur_max, Idx) ->
    max_height(Rest, Cur_max, Idx + 1);
max_height([], Max_Set, _Idx) ->
    Max_Set.


sub_array(List, Left) ->
    sub_array(List, Left, []).

sub_array(_List, Left, Sub_array) when Left == 0 ->
    lists:reverse(Sub_array);
sub_array([Head | Rest], Left, Cur_array) ->
    sub_array(Rest, Left - 1, [Head | Cur_array]).
```