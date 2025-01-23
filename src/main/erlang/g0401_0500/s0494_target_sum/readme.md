[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 494\. Target Sum

Medium

You are given an integer array `nums` and an integer `target`.

You want to build an **expression** out of nums by adding one of the symbols `'+'` and `'-'` before each integer in nums and then concatenate all the integers.

*   For example, if `nums = [2, 1]`, you can add a `'+'` before `2` and a `'-'` before `1` and concatenate them to build the expression `"+2-1"`.

Return the number of different **expressions** that you can build, which evaluates to `target`.

**Example 1:**

**Input:** nums = [1,1,1,1,1], target = 3

**Output:** 5

**Explanation:** There are 5 ways to assign symbols to make the sum of nums be target 3. 

-1 + 1 + 1 + 1 + 1 = 3 

+1 - 1 + 1 + 1 + 1 = 3 

+1 + 1 - 1 + 1 + 1 = 3 

+1 + 1 + 1 - 1 + 1 = 3 

    +1 + 1 + 1 + 1 - 1 = 3

**Example 2:**

**Input:** nums = [1], target = 1

**Output:** 1

**Constraints:**

*   `1 <= nums.length <= 20`
*   `0 <= nums[i] <= 1000`
*   `0 <= sum(nums[i]) <= 1000`
*   `-1000 <= target <= 1000`

## Solution

```erlang
-spec find_target_sum_ways(Nums :: [integer()], Target :: integer()) -> integer().
find_target_sum_ways(Nums, Target) ->
    TotalSum = lists:sum(Nums),
    Sum = TotalSum - Target,
    case Sum < 0 orelse Sum rem 2 =:= 1 of
        true -> 0;
        false -> solve(Nums, Sum div 2)
    end.

-spec solve(Nums :: [integer()], Target :: integer()) -> integer().
solve([First|_] = Nums, Target) ->
    Prev = lists:duplicate(Target + 1, 0),
    InitPrev = case First of
        0 -> lists:sublist([2|lists:duplicate(Target, 0)], Target + 1);
        _ when First =< Target -> 
            lists:sublist([1] ++ lists:duplicate(First - 1, 0) ++ [1] ++ 
                         lists:duplicate(Target - First, 0), Target + 1);
        _ -> [1|lists:duplicate(Target, 0)]
    end,
    process_nums(tl(Nums), Target, InitPrev).

process_nums([], _Target, Prev) ->
    lists:last(Prev);
process_nums([Num|Rest], Target, Prev) ->
    Curr = lists:foldl(fun(J, Acc) ->
        Taken = case J >= Num of
            true -> lists:nth(J - Num + 1, Prev);
            false -> 0
        end,
        NonTaken = lists:nth(J + 1, Prev),
        Acc ++ [Taken + NonTaken]
    end, [], lists:seq(0, Target)),
    process_nums(Rest, Target, Curr).
```