[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 32\. Longest Valid Parentheses

Hard

Given a string containing just the characters `'('` and `')'`, find the length of the longest valid (well-formed) parentheses substring.

**Example 1:**

**Input:** s = "(()"

**Output:** 2

**Explanation:** The longest valid parentheses substring is "()".

**Example 2:**

**Input:** s = ")()())"

**Output:** 4

**Explanation:** The longest valid parentheses substring is "()()".

**Example 3:**

**Input:** s = ""

**Output:** 0

**Constraints:**

*   <code>0 <= s.length <= 3 * 10<sup>4</sup></code>
*   `s[i]` is `'('`, or `')'`.

## Solution

```erlang
-spec longest_valid_parentheses(S :: unicode:unicode_binary()) -> integer().
longest_valid_parentheses(S) ->
    Max1 = scan(S, 0, 0, 0, 1),
    Max2 = scan(reverse_binary(S), 0, 0, 0, -1),
    max(Max1, Max2).

-spec scan(S :: unicode:unicode_binary(), Left :: integer(), Right :: integer(), Max :: integer(), Direction :: integer()) -> integer().
scan(<<>>, _, _, Max, _) -> 
    Max;
scan(<<Ch, Rest/binary>>, Left, Right, Max, Direction) ->
    {NewLeft, NewRight} = 
        case Ch of
            $( -> {Left + 1, Right};
            $) -> {Left, Right + 1};
            _ -> {Left, Right}
        end,
    NewMax = 
        case NewLeft == NewRight of
            true -> max(Max, NewLeft + NewRight);
            false -> Max
        end,
    {ResetLeft, ResetRight} =
        case Direction of
            1 when NewRight > NewLeft -> {0, 0}; % Reset if right > left in forward scan
            -1 when NewLeft > NewRight -> {0, 0}; % Reset if left > right in backward scan
            _ -> {NewLeft, NewRight}
        end,
    scan(Rest, ResetLeft, ResetRight, NewMax, Direction).

% Helper to reverse a binary string manually.
-spec reverse_binary(S :: binary()) -> binary().
reverse_binary(S) -> 
    reverse_binary(S, <<>>).

-spec reverse_binary(S :: binary(), Acc :: binary()) -> binary().
reverse_binary(<<>>, Acc) -> 
    Acc;
reverse_binary(<<Ch, Rest/binary>>, Acc) -> 
    reverse_binary(Rest, <<Ch, Acc/binary>>).

-spec max(A :: integer(), B :: integer()) -> integer().
max(A, B) when A >= B -> A;
max(_, B) -> B.
```