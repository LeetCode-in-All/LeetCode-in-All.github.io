[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 438\. Find All Anagrams in a String

Medium

Given two strings `s` and `p`, return _an array of all the start indices of_ `p`_'s anagrams in_ `s`. You may return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

**Example 1:**

**Input:** s = "cbaebabacd", p = "abc"

**Output:** [0,6]

**Explanation:** 

The substring with start index = 0 is "cba", which is an anagram of "abc". 

The substring with start index = 6 is "bac", which is an anagram of "abc".

**Example 2:**

**Input:** s = "abab", p = "ab"

**Output:** [0,1,2]

**Explanation:** 

The substring with start index = 0 is "ab", which is an anagram of "ab". 

The substring with start index = 1 is "ba", which is an anagram of "ab". 

The substring with start index = 2 is "ab", which is an anagram of "ab".

**Constraints:**

*   <code>1 <= s.length, p.length <= 3 * 10<sup>4</sup></code>
*   `s` and `p` consist of lowercase English letters.

## Solution

```erlang
-spec find_anagrams(S :: unicode:unicode_binary(), P :: unicode:unicode_binary()) -> [integer()].
find_anagrams(S, P) ->
    PLen = byte_size(P),
    SLen = byte_size(S),
    case PLen =< SLen of
        true ->
            Map = init_freq_map(P),
            Window = init_freq_map(binary_part(S, 0, PLen)),
            check_windows(S, PLen, Map, Window, 0, []);
        false ->
            []
    end.

init_freq_map(Bin) ->
    lists:foldl(
        fun(C, Acc) ->
            maps:put(C - $a, maps:get(C - $a, Acc, 0) + 1, Acc)
        end,
        maps:new(),
        binary_to_list(Bin)
    ).

check_windows(S, PLen, Map, Window, I, Result) when I =< byte_size(S) - PLen ->
    NewResult = case maps:to_list(Window) =:= maps:to_list(Map) of
        true -> [I | Result];
        false -> Result
    end,
    case I + PLen of
        SLen when SLen >= byte_size(S) ->
            lists:reverse(NewResult);
        Next ->
            RemoveChar = binary:at(S, I) - $a,
            AddChar = binary:at(S, Next) - $a,
            NewWindow1 = case maps:get(RemoveChar, Window) of
                1 -> maps:remove(RemoveChar, Window);
                N -> maps:put(RemoveChar, N - 1, Window)
            end,
            NewWindow2 = maps:put(AddChar, maps:get(AddChar, NewWindow1, 0) + 1, NewWindow1),
            check_windows(S, PLen, Map, NewWindow2, I + 1, NewResult)
    end;
check_windows(_, _, _, _, _, Result) ->
    lists:reverse(Result).
```