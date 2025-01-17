[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 9\. Palindrome Number

Easy

Given an integer `x`, return `true` if `x` is palindrome integer.

An integer is a **palindrome** when it reads the same backward as forward. For example, `121` is palindrome while `123` is not.

**Example 1:**

**Input:** x = 121

**Output:** true 

**Example 2:**

**Input:** x = -121

**Output:** false

**Explanation:** From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome. 

**Example 3:**

**Input:** x = 10

**Output:** false

**Explanation:** Reads 01 from right to left. Therefore it is not a palindrome. 

**Example 4:**

**Input:** x = -101

**Output:** false 

**Constraints:**

*   <code>-2<sup>31</sup> <= x <= 2<sup>31</sup> - 1</code>

**Follow up:** Could you solve it without converting the integer to a string?

## Solution

```erlang
-spec is_palindrome(X :: integer()) -> boolean().
is_palindrome(X) when X < 0 ->
    false;
is_palindrome(X) ->
    Rev = reverse_number(X, 0),
    Rev == X.

-spec reverse_number(Num :: integer(), Rev :: integer()) -> integer().
reverse_number(0, Rev) ->
    Rev;
reverse_number(Num, Rev) ->
    Digit = Num rem 10,
    NewRev = Rev * 10 + Digit,
    reverse_number(Num div 10, NewRev).
```