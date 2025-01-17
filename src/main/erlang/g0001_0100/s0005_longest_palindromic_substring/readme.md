[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 5\. Longest Palindromic Substring

Medium

Given a string `s`, return _the longest palindromic substring_ in `s`.

**Example 1:**

**Input:** s = "babad"

**Output:** "bab" **Note:** "aba" is also a valid answer. 

**Example 2:**

**Input:** s = "cbbd"

**Output:** "bb" 

**Example 3:**

**Input:** s = "a"

**Output:** "a" 

**Example 4:**

**Input:** s = "ac"

**Output:** "a" 

**Constraints:**

*   `1 <= s.length <= 1000`
*   `s` consist of only digits and English letters.

## Solution

```erlang
-spec longest_palindrome(S :: unicode:unicode_binary()) -> unicode:unicode_binary().
longest_palindrome(S) ->
    Length = byte_size(S),
    case Length of
        0 -> <<>>; % Return empty binary if input is empty
        _ ->
            % Initialize variables for the best palindrome
            {Start, Len} = lists:foldl(
                fun(Index, {BestStart, BestLen}) ->
                    % Find the longest palindrome for odd and even length centers
                    {NewStart1, NewLen1} = find_longest_palindrome(S, Index, Index),
                    {NewStart2, NewLen2} = find_longest_palindrome(S, Index, Index + 1),
                    % Choose the longer of the two found palindromes
                    case NewLen1 >= NewLen2 of
                        true  -> update_best(BestStart, BestLen, NewStart1, NewLen1);
                        false -> update_best(BestStart, BestLen, NewStart2, NewLen2)
                    end
                end,
                {0, 0}, % Initial best palindrome start and length
                lists:seq(0, Length - 1) % Iterate through all positions
            ),
            % Extract the longest palindromic substring
            binary:part(S, Start, Len)
    end.

% Helper function to find the longest palindrome around the center
-spec find_longest_palindrome(S :: unicode:unicode_binary(), L :: integer(), R :: integer()) -> {integer(), integer()}.
find_longest_palindrome(S, L, R) ->
    Length = byte_size(S),
    case (L >= 0 andalso R < Length andalso binary:part(S, L, 1) =:= binary:part(S, R, 1)) of
        true ->
            find_longest_palindrome(S, L - 1, R + 1);
        false ->
            {L + 1, R - L - 1}
    end.

% Helper function to update the best palindrome found so far
-spec update_best(BestStart :: integer(), BestLen :: integer(), NewStart :: integer(), NewLen :: integer()) -> {integer(), integer()}.
update_best(BestStart, BestLen, NewStart, NewLen) ->
    case NewLen > BestLen of
        true  -> {NewStart, NewLen};
        false -> {BestStart, BestLen}
    end.
```