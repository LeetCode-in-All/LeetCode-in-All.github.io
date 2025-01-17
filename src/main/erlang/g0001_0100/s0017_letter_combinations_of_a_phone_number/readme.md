[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 17\. Letter Combinations of a Phone Number

Medium

Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent. Return the answer in **any order**.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)

**Example 1:**

**Input:** digits = "23"

**Output:** ["ad","ae","af","bd","be","bf","cd","ce","cf"]

**Example 2:**

**Input:** digits = ""

**Output:** []

**Example 3:**

**Input:** digits = "2"

**Output:** ["a","b","c"]

**Constraints:**

*   `0 <= digits.length <= 4`
*   `digits[i]` is a digit in the range `['2', '9']`.

## Solution

```erlang
-spec letter_combinations(Digits :: unicode:unicode_binary()) -> [unicode:unicode_binary()].
letter_combinations(Digits) ->
    Res = lists:foldl(fun(Digit, Acc) -> 
        case Digit of
            <<"2">> -> 
                [<<Accbin/binary, Byte/binary>> || Byte <- [<<A>> || <<A:8>> <= <<"abc">>], Accbin <- Acc];
            <<"3">> -> 
                [<<Accbin/binary, Byte/binary>> || Byte <- [<<A>> || <<A:8>> <= <<"def">>], Accbin <- Acc];
            <<"4">> -> 
                [<<Accbin/binary, Byte/binary>> || Byte <- [<<A>> || <<A:8>> <= <<"ghi">>], Accbin <- Acc];
            <<"5">> -> 
                [<<Accbin/binary, Byte/binary>> || Byte <- [<<A>> || <<A:8>> <= <<"jkl">>], Accbin <- Acc];
            <<"6">> -> 
                [<<Accbin/binary, Byte/binary>> || Byte <- [<<A>> || <<A:8>> <= <<"mno">>], Accbin <- Acc];
            <<"7">> -> 
                [<<Accbin/binary, Byte/binary>> || Byte <- [<<A>> || <<A:8>> <= <<"pqrs">>], Accbin <- Acc];
            <<"8">> -> 
                [<<Accbin/binary, Byte/binary>> || Byte <- [<<A>> || <<A:8>> <= <<"tuv">>], Accbin <- Acc];
            <<"9">> -> 
                [<<Accbin/binary, Byte/binary>> || Byte <- [<<A>> || <<A:8>> <= <<"wxyz">>], Accbin <- Acc]
        end
    end, [<<>>], [<<B>> || <<B:8>> <= Digits]),
    case Res of
        [<<>>] -> [];
        _ -> Res
    end.
```