[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 394\. Decode String

Medium

Given an encoded string, return its decoded string.

The encoding rule is: `k[encoded_string]`, where the `encoded_string` inside the square brackets is being repeated exactly `k` times. Note that `k` is guaranteed to be a positive integer.

You may assume that the input string is always valid; there are no extra white spaces, square brackets are well-formed, etc. Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, `k`. For example, there will not be input like `3a` or `2[4]`.

The test cases are generated so that the length of the output will never exceed <code>10<sup>5</sup></code>.

**Example 1:**

**Input:** s = "3[a]2[bc]"

**Output:** "aaabcbc"

**Example 2:**

**Input:** s = "3[a2[c]]"

**Output:** "accaccacc"

**Example 3:**

**Input:** s = "2[abc]3[cd]ef"

**Output:** "abcabccdcdcdef"

**Constraints:**

*   `1 <= s.length <= 30`
*   `s` consists of lowercase English letters, digits, and square brackets `'[]'`.
*   `s` is guaranteed to be **a valid** input.
*   All the integers in `s` are in the range `[1, 300]`.

## Solution

```erlang
-spec decode_string(S :: unicode:unicode_binary()) -> unicode:unicode_binary().
decode_string(S) ->
    decode_helper(S, 1).

decode_helper(S, I) when I > byte_size(S) ->
    <<>>;
decode_helper(S, I) ->
    decode_helper(S, I, 0, <<>>).

decode_helper(S, I, _Count, Acc) when I > byte_size(S) ->
    Acc;
decode_helper(S, I, Count, Acc) ->
    case binary:at(S, I-1) of
        C when C >= $a, C =< $z; C >= $A, C =< $Z ->
            decode_helper(S, I+1, Count, <<Acc/binary, C>>);
        C when C >= $0, C =< $9 ->
            NewCount = Count * 10 + (C - $0),
            decode_helper(S, I+1, NewCount, Acc);
        $[ ->
            {Repeated, NextI} = decode_bracket(S, I+1),
            RepeatedStr = repeat_string(Repeated, Count),
            decode_helper(S, NextI, 0, <<Acc/binary, RepeatedStr/binary>>);
        _ ->
            decode_helper(S, I+1, Count, Acc)
    end.

decode_bracket(S, I) ->
    decode_bracket(S, I, 0, <<>>).

decode_bracket(S, I, Count, Acc) when I > byte_size(S) ->
    {Acc, I};
decode_bracket(S, I, Count, Acc) ->
    case binary:at(S, I-1) of
        C when C >= $a, C =< $z; C >= $A, C =< $Z ->
            decode_bracket(S, I+1, Count, <<Acc/binary, C>>);
        C when C >= $0, C =< $9 ->
            NewCount = Count * 10 + (C - $0),
            decode_bracket(S, I+1, NewCount, Acc);
        $[ ->
            {Repeated, NextI} = decode_bracket(S, I+1),
            RepeatedStr = repeat_string(Repeated, Count),
            decode_bracket(S, NextI, 0, <<Acc/binary, RepeatedStr/binary>>);
        $] ->
            {Acc, I+1};
        _ ->
            decode_bracket(S, I+1, Count, Acc)
    end.

repeat_string(Str, Count) ->
    repeat_string(Str, Count, <<>>).

repeat_string(_, 0, Acc) ->
    Acc;
repeat_string(Str, Count, Acc) ->
    repeat_string(Str, Count-1, <<Acc/binary, Str/binary>>).
```