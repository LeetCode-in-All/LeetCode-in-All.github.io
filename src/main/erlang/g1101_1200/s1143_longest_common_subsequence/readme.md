[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 1143\. Longest Common Subsequence

Medium

Given two strings `text1` and `text2`, return _the length of their longest **common subsequence**._ If there is no **common subsequence**, return `0`.

A **subsequence** of a string is a new string generated from the original string with some characters (can be none) deleted without changing the relative order of the remaining characters.

*   For example, `"ace"` is a subsequence of `"abcde"`.

A **common subsequence** of two strings is a subsequence that is common to both strings.

**Example 1:**

**Input:** text1 = "abcde", text2 = "ace"

**Output:** 3

**Explanation:** The longest common subsequence is "ace" and its length is 3.

**Example 2:**

**Input:** text1 = "abc", text2 = "abc"

**Output:** 3

**Explanation:** The longest common subsequence is "abc" and its length is 3.

**Example 3:**

**Input:** text1 = "abc", text2 = "def"

**Output:** 0

**Explanation:** There is no such common subsequence, so the result is 0.

**Constraints:**

*   `1 <= text1.length, text2.length <= 1000`
*   `text1` and `text2` consist of only lowercase English characters.

## Solution

```erlang
-spec longest_common_subsequence(Text1 :: unicode:unicode_binary(), Text2 :: unicode:unicode_binary()) -> integer().
longest_common_subsequence(Text1, Text2) ->
    S1 = binary_to_list(Text1),
    S2 = binary_to_list(Text2),
    Key = {length(S1) - 1, length(S2) - 1},
    Memo = #{},
    maps:get(Key, recur(Memo, S1, S2, Key), 0).

-spec recur(map(), list(), list(), {integer(), integer()}) -> map().
recur(Memo, [], _, Key) ->
    maps:put(Key, 0, Memo);
recur(Memo, _, [], Key) ->
    maps:put(Key, 0, Memo);
recur(Memo, [X | Xs] = Xss, [Y | Ys] = Yss, {I, J} = Key) ->
    case maps:is_key(Key, Memo) of
        true ->
            Memo;
        false ->
            if
                X =:= Y ->
                    Memo1 = recur(Memo, Xs, Ys, {I - 1, J - 1}),
                    maps:put(Key, 1 + maps:get({I - 1, J - 1}, Memo1, 0), Memo1);
                true ->
                    Memo1 = recur(Memo, Xss, Ys, {I, J - 1}),
                    Memo2 = recur(Memo1, Xs, Yss, {I - 1, J}),
                    maps:put(Key, max(maps:get({I, J - 1}, Memo2, 0), maps:get({I - 1, J}, Memo2, 0)), Memo2)
            end
    end.
```