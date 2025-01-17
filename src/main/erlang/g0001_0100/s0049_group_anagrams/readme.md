[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 49\. Group Anagrams

Medium

Given an array of strings `strs`, group **the anagrams** together. You can return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

**Example 1:**

**Input:** strs = ["eat","tea","tan","ate","nat","bat"]

**Output:** [["bat"],["nat","tan"],["ate","eat","tea"]]

**Example 2:**

**Input:** strs = [""]

**Output:** [[""]]

**Example 3:**

**Input:** strs = ["a"]

**Output:** [["a"]]

**Constraints:**

*   <code>1 <= strs.length <= 10<sup>4</sup></code>
*   `0 <= strs[i].length <= 100`
*   `strs[i]` consists of lowercase English letters.

## Solution

```erlang
-spec group_anagrams(Strs :: [unicode:unicode_binary()]) -> [[unicode:unicode_binary()]].
group_anagrams(Strs) ->
    AnagramMap = group_anagrams_helper(Strs, #{}),
    maps:values(AnagramMap).

group_anagrams_helper([Head | Tail], Acc) ->
    NewString = sort_string(Head),
    NewMap = case maps:is_key(NewString, Acc) of
        true ->
            maps:update(NewString, [Head | maps:get(NewString, Acc)], Acc);
        false ->
            maps:put(NewString, [Head], Acc)
    end,
    group_anagrams_helper(Tail, NewMap);
group_anagrams_helper([], Acc) ->
    Acc.

sort_string(Str) ->
    StrList = binary_to_list(Str),        % Convert string to list of characters
    SortedList = lists:sort(StrList),       % Sort the list of characters
    list_to_binary(SortedList).
```