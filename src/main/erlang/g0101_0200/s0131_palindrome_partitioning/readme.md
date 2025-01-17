[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 131\. Palindrome Partitioning

Medium

Given a string `s`, partition `s` such that every substring of the partition is a **palindrome**. Return all possible palindrome partitioning of `s`.

A **palindrome** string is a string that reads the same backward as forward.

**Example 1:**

**Input:** s = "aab"

**Output:** [["a","a","b"],["aa","b"]]

**Example 2:**

**Input:** s = "a"

**Output:** [["a"]]

**Constraints:**

*   `1 <= s.length <= 16`
*   `s` contains only lowercase English letters.

## Solution

```erlang
-spec partition(S :: unicode:unicode_binary()) -> [[unicode:unicode_binary()]].
partition(S) ->
    Len = byte_size(S),
    dfs(S, Len, 0, [], []).

% Base case: when we've processed the entire string
dfs(_S, Len, L, Subs, Ans) when L =:= Len ->
    [lists:reverse(Subs) | Ans];

% Recursive case: try all possible partitions
dfs(S, Len, L, Subs, Ans) ->
    partition_from_position(S, Len, L, L, Subs, Ans).

partition_from_position(S, Len, L, R, Subs, Ans) when R < Len ->
    Substring = binary:part(S, L, R - L + 1),
    NewAns = case is_palindrome(Substring) of
        true -> 
            dfs(S, Len, R + 1, [Substring | Subs], Ans);
        false -> 
            Ans
    end,
    partition_from_position(S, Len, L, R + 1, Subs, NewAns);
partition_from_position(_S, _Len, _L, _R, _Subs, Ans) ->
    Ans.

% Helper function to check if a binary is a palindrome
is_palindrome(Bin) ->
    List = binary_to_list(Bin),
    List =:= lists:reverse(List).
```