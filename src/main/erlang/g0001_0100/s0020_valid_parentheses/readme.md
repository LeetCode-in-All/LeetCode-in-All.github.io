[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 20\. Valid Parentheses

Easy

Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1.  Open brackets must be closed by the same type of brackets.
2.  Open brackets must be closed in the correct order.

**Example 1:**

**Input:** s = "()"

**Output:** true

**Example 2:**

**Input:** s = "()[]{}"

**Output:** true

**Example 3:**

**Input:** s = "(]"

**Output:** false

**Example 4:**

**Input:** s = "([)]"

**Output:** false

**Example 5:**

**Input:** s = "{[]}"

**Output:** true

**Constraints:**

*   <code>1 <= s.length <= 10<sup>4</sup></code>
*   `s` consists of parentheses only `'()[]{}'`.

## Solution

```erlang
%% Check if binary has valid parentheses
-spec is_valid(S :: unicode:unicode_binary()) -> boolean().
is_valid(S) ->
    process_binary(S, []).

%% Process binary with stack, where empty list is empty stack
-spec process_binary(binary(), list()) -> boolean().
process_binary(<<>>, []) -> 
    true;
process_binary(<<>>, _Stack) -> 
    false;
process_binary(<<Char/utf8, Rest/binary>>, Stack) ->
    case Char of
        40 -> process_binary(Rest, [40 | Stack]);  % '('
        91 -> process_binary(Rest, [91 | Stack]);  % '['
        123 -> process_binary(Rest, [123 | Stack]);  % '{'
        41 -> % ')'
            case Stack of
                [40 | NewStack] -> process_binary(Rest, NewStack);
                _ -> false
            end;
        93 -> % ']'
            case Stack of
                [91 | NewStack] -> process_binary(Rest, NewStack);
                _ -> false
            end;
        125 -> % '}'
            case Stack of
                [123 | NewStack] -> process_binary(Rest, NewStack);
                _ -> false
            end;
        _ -> false  % Invalid character
    end.
```