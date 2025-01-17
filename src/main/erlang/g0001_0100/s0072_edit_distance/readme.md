[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 72\. Edit Distance

Hard

Given two strings `word1` and `word2`, return _the minimum number of operations required to convert `word1` to `word2`_.

You have the following three operations permitted on a word:

*   Insert a character
*   Delete a character
*   Replace a character

**Example 1:**

**Input:** word1 = "horse", word2 = "ros"

**Output:** 3

**Explanation:** 

horse -> rorse (replace 'h' with 'r') 

rorse -> rose (remove 'r') 

rose -> ros (remove 'e')

**Example 2:**

**Input:** word1 = "intention", word2 = "execution"

**Output:** 5

**Explanation:** 

intention -> inention (remove 't') 

inention -> enention (replace 'i' with 'e') 

enention -> exention (replace 'n' with 'x') 

exention -> exection (replace 'n' with 'c') 

exection -> execution (insert 'u')

**Constraints:**

*   `0 <= word1.length, word2.length <= 500`
*   `word1` and `word2` consist of lowercase English letters.

## Solution

```erlang
-spec min_distance(Word1 :: unicode:unicode_binary(), Word2 :: unicode:unicode_binary()) -> integer().
min_distance(Word1, Word2) ->
    Word1List = [" " | unicode:characters_to_list(Word1)],
    Word2List = [" " | unicode:characters_to_list(Word2)],
    Len1 = length(Word1List) - 1,
    Len2 = length(Word2List) - 1,
    
    Map = build_distance_map(Word1List, Word2List),
    maps:get({Len1, Len2}, Map).

build_distance_map(Word1List, Word2List) ->
    Indices1 = lists:zip(Word1List, lists:seq(0, length(Word1List) - 1)),
    Indices2 = lists:zip(Word2List, lists:seq(0, length(Word2List) - 1)),
    lists:foldl(
        fun({Ch1, I}, MapAcc1) ->
            lists:foldl(
                fun({Ch2, J}, MapAcc2) ->
                    Value = calculate_distance(Ch1, Ch2, I, J, MapAcc2),
                    maps:put({I, J}, Value, MapAcc2)
                end,
                MapAcc1,
                Indices2
            )
        end,
        maps:new(),
        Indices1
    ).

calculate_distance(_, _, 0, J, _) -> J;
calculate_distance(_, _, I, 0, _) -> I;
calculate_distance(Ch, Ch, I, J, Map) ->
    maps:get({I-1, J-1}, Map);
calculate_distance(_, _, I, J, Map) ->
    Min1 = min(maps:get({I-1, J}, Map), maps:get({I-1, J-1}, Map)),
    Min2 = min(Min1, maps:get({I, J-1}, Map)),
    Min2 + 1.
```