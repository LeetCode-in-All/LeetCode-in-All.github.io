[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 22\. Generate Parentheses

Medium

Given `n` pairs of parentheses, write a function to _generate all combinations of well-formed parentheses_.

**Example 1:**

**Input:** n = 3

**Output:** ["((()))","(()())","(())()","()(())","()()()"]

**Example 2:**

**Input:** n = 1

**Output:** ["()"]

**Constraints:**

*   `1 <= n <= 8`

## Solution

```erlang
%% Generate all valid parenthesis combinations
-spec generate_parenthesis(N :: integer()) -> [unicode:unicode_binary()].
generate_parenthesis(N) ->
    generate(N, N, [], []).

%% Helper function that builds combinations recursively
-spec generate(Open :: integer(), Close :: integer(), 
              Current :: list(), Acc :: [unicode:unicode_binary()]) -> [unicode:unicode_binary()].
generate(0, 0, Current, Acc) ->
    % Convert the reversed list of characters to a binary
    [list_to_binary(lists:reverse(Current)) | Acc];
generate(Open, Close, Current, Acc) when Open > 0 ->
    % Try adding an opening parenthesis
    NewAcc1 = generate(Open - 1, Close, [$( | Current], Acc),
    % If we can add a closing parenthesis, try that branch too
    case Close > Open of
        true -> generate(Open, Close - 1, [$) | Current], NewAcc1);
        false -> NewAcc1
    end;
generate(Open, Close, Current, Acc) when Close > Open ->
    % Can only add a closing parenthesis
    generate(Open, Close - 1, [$) | Current], Acc).
```