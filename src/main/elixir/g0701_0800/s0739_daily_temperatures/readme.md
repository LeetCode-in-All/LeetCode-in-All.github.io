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

```elixir
defmodule Solution do
  @spec daily_temperatures(temp :: [integer]) :: [integer]
  def daily_temperatures(temp) do
    Enum.reverse(temp)
    |> Enum.with_index()
    |> Enum.map_reduce([], &do_map_reduce/2)
    |> elem(0)
    |> Enum.reverse()
  end

  defp do_map_reduce({x, i}, [{y, j} | tail]) when x >= y do
    do_map_reduce({x, i}, tail)
  end
  defp do_map_reduce({x, i}, [{y, j} | tail]) do
    {i - j, [{x, i}, {y, j} | tail]}
  end
  defp do_map_reduce({x, i}, []) do
    {0, [{x, i}]}
  end
end
```