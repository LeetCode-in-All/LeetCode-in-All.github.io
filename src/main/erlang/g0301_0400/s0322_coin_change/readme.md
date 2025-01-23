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

```erlang
-spec coin_change(Coins :: [integer()], Amount :: integer()) -> integer().
coin_change(Coins, Amount) ->
    % Sort coins in ascending order
    SortedCoins = lists:sort(Coins),
    
    % Initialize DP map with base case
    InitDP = #{0 => 0},
    
    % Build DP table for amounts from 1 to target
    case Amount of
        0 -> 0;
        _ ->
            FinalDP = build_dp_table(SortedCoins, lists:seq(1, Amount), InitDP),
            % Get result or return -1 if not possible
            maps:get(Amount, FinalDP, -1)
    end.

% Build DP table for all amounts
-spec build_dp_table([integer()], [integer()], map()) -> map().
build_dp_table(_Coins, [], DP) -> DP;
build_dp_table(Coins, [Amount|Rest], DP) ->
    NewDP = process_coins_for_amount(Coins, Amount, DP),
    build_dp_table(Coins, Rest, NewDP).

% Process all coins for current amount
-spec process_coins_for_amount([integer()], integer(), map()) -> map().
process_coins_for_amount([], _Amount, DP) -> DP;
process_coins_for_amount([Coin|Rest], Amount, DP) ->
    case Coin > Amount of
        true ->
            % Stop if coin is larger than current amount
            DP;
        false ->
            % Try using current coin
            case maps:get(Amount - Coin, DP, undefined) of
                undefined ->
                    % Can't use this coin, try next
                    process_coins_for_amount(Rest, Amount, DP);
                PrevCount ->
                    % Can use this coin, update minimum coins needed
                    NewCount = PrevCount + 1,
                    NewDP = maps:update_with(Amount, 
                                           fun(OldVal) -> min(OldVal, NewCount) end,
                                           NewCount, 
                                           DP),
                    process_coins_for_amount(Rest, Amount, NewDP)
            end
    end.
```