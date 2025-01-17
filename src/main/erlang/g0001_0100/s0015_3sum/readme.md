[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 15\. 3Sum

Medium

Given an integer array nums, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

**Example 1:**

**Input:** nums = [-1,0,1,2,-1,-4]

**Output:** [[-1,-1,2],[-1,0,1]] 

**Example 2:**

**Input:** nums = []

**Output:** [] 

**Example 3:**

**Input:** nums = [0]

**Output:** [] 

**Constraints:**

*   `0 <= nums.length <= 3000`
*   <code>-10<sup>5</sup> <= nums[i] <= 10<sup>5</sup></code>

## Solution

```erlang
-spec three_sum(Nums :: [integer()]) -> [[integer()]].

three_sum(Nums) ->
    NumsSet     = sets:from_list(Nums),

    GroupedNums = maps:groups_from_list(fun(N)->if N>0->1; N<0->-1; true->0 end end, Nums),
    Negatives   = maps:get(-1, GroupedNums, []),
    Zeroes      = maps:get( 0, GroupedNums, []),
    Positives   = maps:get( 1, GroupedNums, []),
    NumZeroes   = length(Zeroes),

    {UniquePositive, UniquePositivePairs} = unique_pairs(Positives),
    {             _, UniqueNegativePairs} = unique_pairs(Negatives),

    SameSign     =  UniquePositivePairs ++ UniqueNegativePairs,

    NonZeroTriplets = [[A,B,-A-B] || {A,B} <- SameSign, sets:is_element(-A-B,NumsSet)],
    OneZeroTriplets =
        if NumZeroes>0 -> [[A,-A,0] || A <- UniquePositive, sets:is_element(-A,NumsSet)];
           true -> []
        end,
    ZeroTriplets = if NumZeroes>2 -> [[0,0,0]]; true-> [] end,
    NonZeroTriplets ++ OneZeroTriplets ++ ZeroTriplets.

unique_pairs(Nums) ->
    NumGroups    = maps:groups_from_list(fun(N)->N end, Nums),
    UniqueNums   = maps:keys(NumGroups),
    RepeatedNums = [{N,N} || N<-UniqueNums, length(maps:get(N,NumGroups))>1],
    {UniqueNums, pairs(UniqueNums,[]) ++ RepeatedNums}.

pairs([],Acc) -> lists:append(Acc);
pairs([H|T],Acc) -> pairs(T, [[{H,X}||X<-T]|Acc]).
```