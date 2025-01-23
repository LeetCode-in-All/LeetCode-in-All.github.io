[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 139\. Word Break

Medium

Given a string `s` and a dictionary of strings `wordDict`, return `true` if `s` can be segmented into a space-separated sequence of one or more dictionary words.

**Note** that the same word in the dictionary may be reused multiple times in the segmentation.

**Example 1:**

**Input:** s = "leetcode", wordDict = ["leet","code"]

**Output:** true

**Explanation:** Return true because "leetcode" can be segmented as "leet code".

**Example 2:**

**Input:** s = "applepenapple", wordDict = ["apple","pen"]

**Output:** true

**Explanation:** Return true because "applepenapple" can be segmented as "apple pen apple". 

Note that you are allowed to reuse a dictionary word.

**Example 3:**

**Input:** s = "catsandog", wordDict = ["cats","dog","sand","and","cat"]

**Output:** false

**Constraints:**

*   `1 <= s.length <= 300`
*   `1 <= wordDict.length <= 1000`
*   `1 <= wordDict[i].length <= 20`
*   `s` and `wordDict[i]` consist of only lowercase English letters.
*   All the strings of `wordDict` are **unique**.

## Solution

```erlang
-spec word_break(S :: unicode:unicode_binary(), WordDict :: [unicode:unicode_binary()]) -> boolean().
word_break(S, WordDict) ->
    % Initialize ETS table for memoization
    ets:new(memo, [set, named_table]),
    % Process word dict to include sizes
    Words = [{Word, byte_size(Word)} || Word <- WordDict],
    % Get result
    Result = breakable(S, Words),
    % Clean up
    ets:delete(memo),
    Result.

-spec breakable(binary(), [{binary(), integer()}]) -> boolean().
breakable(<<>>, _Words) ->
    true;
breakable(S, Words) ->
    case ets:lookup(memo, S) of
        [{_, Result}] ->
            Result;
        [] ->
            Result = try_words(S, Words, Words),
            ets:insert(memo, {S, Result}),
            Result
    end.

try_words(_S, [], _AllWords) ->
    false;
try_words(S, [{Word, Len} | Rest], AllWords) ->
    case S of
        <<Prefix:Len/binary, Remaining/binary>> when Prefix =:= Word ->
            case breakable(Remaining, AllWords) of
                true -> true;
                false -> try_words(S, Rest, AllWords)
            end;
        _ ->
            try_words(S, Rest, AllWords)
    end.
```