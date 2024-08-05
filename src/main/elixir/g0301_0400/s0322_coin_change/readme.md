[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 322\. Coin Change

Medium

You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money.

Return _the fewest number of coins that you need to make up that amount_. If that amount of money cannot be made up by any combination of the coins, return `-1`.

You may assume that you have an infinite number of each kind of coin.

**Example 1:**

**Input:** coins = [1,2,5], amount = 11

**Output:** 3

**Explanation:** 11 = 5 + 5 + 1

**Example 2:**

**Input:** coins = [2], amount = 3

**Output:** -1

**Example 3:**

**Input:** coins = [1], amount = 0

**Output:** 0

**Constraints:**

*   `1 <= coins.length <= 12`
*   <code>1 <= coins[i] <= 2<sup>31</sup> - 1</code>
*   <code>0 <= amount <= 10<sup>4</sup></code>

## Solution

```elixir
defmodule Solution do
  @spec coin_change(coins :: [integer], amount :: integer) :: integer
  def coin_change(coins, amount) do
    coins = Enum.sort(coins)

    for a <- 1..amount, reduce: %{0 => 0} do
      dp ->
        coins
        |> Enum.reduce_while(dp, fn c, dp ->
          cond do
            c > a ->
              {:halt, dp}

            dp[a - c] != nil ->
              {:cont, Map.update(dp, a, dp[a - c] + 1, &min(&1, dp[a - c] + 1))}

            true ->
              {:cont, dp}
          end
        end)
    end
    |> Map.get(amount, -1)
  end
end
```