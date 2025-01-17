[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 647\. Palindromic Substrings

Medium

Given a string `s`, return _the number of **palindromic substrings** in it_.

A string is a **palindrome** when it reads the same backward as forward.

A **substring** is a contiguous sequence of characters within the string.

**Example 1:**

**Input:** s = "abc"

**Output:** 3

**Explanation:** Three palindromic strings: "a", "b", "c".

**Example 2:**

**Input:** s = "aaa"

**Output:** 6

**Explanation:** Six palindromic strings: "a", "a", "a", "aa", "aa", "aaa".

**Constraints:**

*   `1 <= s.length <= 1000`
*   `s` consists of lowercase English letters.

## Solution

```erlang
-spec count_substrings(S :: binary()) -> integer().
count_substrings(S) ->
    TupleS = list_to_tuple(unicode:characters_to_list(S)),
    get_count(TupleS, 0, 0).

-spec get_count(TupleS :: tuple(), Count :: integer(), I :: integer()) -> integer().
get_count(TupleS, Count, I) when I >= tuple_size(TupleS) ->
    Count;
get_count(TupleS, Count, I) ->
    Left = I,
    Right = I,
    Count1 = Count + while(TupleS, 0, Left, Right),
    Left1 = I,
    Right1 = I + 1,
    Count2 = Count1 + while(TupleS, 0, Left1, Right1),
    get_count(TupleS, Count2, I + 1).

-spec while(TupleS :: tuple(), Acc :: integer(), Left :: integer(), Right :: integer()) -> integer().
while(TupleS, Acc, Left, Right) when Left < 0; Right >= tuple_size(TupleS); element(Left + 1, TupleS) /= element(Right + 1, TupleS) ->
    Acc;
while(TupleS, Acc, Left, Right) ->
    while(TupleS, Acc + 1, Left - 1, Right + 1).
```