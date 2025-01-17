[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 10\. Regular Expression Matching

Hard

Given an input string `s` and a pattern `p`, implement regular expression matching with support for `'.'` and `'*'` where:

*   `'.'` Matches any single character.
*   `'*'` Matches zero or more of the preceding element.

The matching should cover the **entire** input string (not partial).

**Example 1:**

**Input:** s = "aa", p = "a"

**Output:** false

**Explanation:** "a" does not match the entire string "aa". 

**Example 2:**

**Input:** s = "aa", p = "a\*"

**Output:** true

**Explanation:** '\*' means zero or more of the preceding element, 'a'. Therefore, by repeating 'a' once, it becomes "aa". 

**Example 3:**

**Input:** s = "ab", p = ".\*"

**Output:** true

**Explanation:** ".\*" means "zero or more (\*) of any character (.)". 

**Example 4:**

**Input:** s = "aab", p = "c\*a\*b"

**Output:** true

**Explanation:** c can be repeated 0 times, a can be repeated 1 time. Therefore, it matches "aab". 

**Example 5:**

**Input:** s = "mississippi", p = "mis\*is\*p\*."

**Output:** false 

**Constraints:**

*   `1 <= s.length <= 20`
*   `1 <= p.length <= 30`
*   `s` contains only lowercase English letters.
*   `p` contains only lowercase English letters, `'.'`, and `'*'`.
*   It is guaranteed for each appearance of the character `'*'`, there will be a previous valid character to match.

## Solution

```erlang
-spec is_match(S :: unicode:unicode_binary(), P :: unicode:unicode_binary()) -> boolean().
is_match(S, P) ->
    match(S, compile(P)).

compile(PatternStr) ->
    compile(PatternStr, []).

compile(<<>>, Acc) ->
    lists:reverse(Acc);
compile(<<Char, $*, Rest/binary>>, Acc) ->
    compile(Rest, [{star, Char}|Acc]);
compile(<<Char, Rest/binary>>, Acc) ->
    compile(Rest, [{single, Char}|Acc]).


match(<<>>, [])  -> true;
match(_,    [])  -> false;
match(<<>>, Pattern)  ->
    lists:all(fun F(E) -> {Type,_}=E, Type==star end, Pattern);
match(Text, Pattern) ->
    <<Char, Rest/binary>> = Text,
    [{MatchType, MatchChar}|PatternRest] = Pattern,
    case {MatchType, (Char==MatchChar) or (MatchChar==$.)} of
        {single, true } -> match(Rest, PatternRest);
        {single, false} -> false;
        {star,   true } -> case (match(Rest, Pattern)) of
                               true  -> true;
                               false -> match(Text, PatternRest)
                           end;
        {star,   false} -> match(Text, PatternRest)
    end.
```