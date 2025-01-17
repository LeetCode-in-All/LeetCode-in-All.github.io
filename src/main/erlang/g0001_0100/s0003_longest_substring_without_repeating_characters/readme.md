[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 3\. Longest Substring Without Repeating Characters

Medium

Given a string `s`, find the length of the **longest substring** without repeating characters.

**Example 1:**

**Input:** s = "abcabcbb"

**Output:** 3

**Explanation:** The answer is "abc", with the length of 3. 

**Example 2:**

**Input:** s = "bbbbb"

**Output:** 1

**Explanation:** The answer is "b", with the length of 1. 

**Example 3:**

**Input:** s = "pwwkew"

**Output:** 3

**Explanation:** The answer is "wke", with the length of 3. Notice that the answer must be a substring, "pwke" is a subsequence and not a substring. 

**Example 4:**

**Input:** s = ""

**Output:** 0 

**Constraints:**

*   <code>0 <= s.length <= 5 * 10<sup>4</sup></code>
*   `s` consists of English letters, digits, symbols and spaces.

## Solution

```erlang
-spec length_of_longest_substring(S :: unicode:unicode_binary()) -> integer().
length_of_longest_substring(S) ->
    do(S, 0, #{}, 0, 1).

do(<<Char, Rest/binary>>, Index, PrevPos, Max, Acc0) when is_map_key(Char, PrevPos) ->
    PrevIndex = map_get(Char, PrevPos),
    Acc1 = Index - PrevIndex,
    Acc = min(Acc1, Acc0),
    do(Rest, Index + 1, PrevPos#{Char => Index}, max(Max, Acc), Acc + 1);
do(<<Char, Rest/binary>>, Index, PrevPos, Max, Acc) when Acc > Max ->
    do(Rest, Index + 1, PrevPos#{Char => Index}, Acc, Acc + 1);
do(<<Char, Rest/binary>>, Index, PrevPos, Max, Acc) ->
    do(Rest, Index + 1, PrevPos#{Char => Index}, Max, Acc + 1);

do(<<>>, _, _, Max, _) -> Max.
```