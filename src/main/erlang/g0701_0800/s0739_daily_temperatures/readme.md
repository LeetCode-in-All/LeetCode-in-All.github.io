[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 739\. Daily Temperatures

Medium

Given an array of integers `temperatures` represents the daily temperatures, return _an array_ `answer` _such that_ `answer[i]` _is the number of days you have to wait after the_ <code>i<sup>th</sup></code> _day to get a warmer temperature_. If there is no future day for which this is possible, keep `answer[i] == 0` instead.

**Example 1:**

**Input:** temperatures = [73,74,75,71,69,72,76,73]

**Output:** [1,1,4,2,1,1,0,0]

**Example 2:**

**Input:** temperatures = [30,40,50,60]

**Output:** [1,1,1,0]

**Example 3:**

**Input:** temperatures = [30,60,90]

**Output:** [1,1,0]

**Constraints:**

*   <code>1 <= temperatures.length <= 10<sup>5</sup></code>
*   `30 <= temperatures[i] <= 100`

## Solution

```erlang
-spec daily_temperatures([integer()]) -> [integer()].
daily_temperatures(Temp) ->
    {Result, _} = lists:mapfoldl(fun do_map_reduce/2, [], lists:zip(lists:reverse(Temp), lists:seq(0, length(Temp) - 1))),
    lists:reverse(Result).

do_map_reduce({X, I}, [{Y, J} | Tail]) when X >= Y ->
    do_map_reduce({X, I}, Tail);
do_map_reduce({X, I}, [{Y, J} | Tail]) ->
    {I - J, [{X, I}, {Y, J} | Tail]};
do_map_reduce({X, I}, []) ->
    {0, [{X, I}]}.
```