[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 763\. Partition Labels

Medium

You are given a string `s`. We want to partition the string into as many parts as possible so that each letter appears in at most one part.

Note that the partition is done so that after concatenating all the parts in order, the resultant string should be `s`.

Return _a list of integers representing the size of these parts_.

**Example 1:**

**Input:** s = "ababcbacadefegdehijhklij"

**Output:** [9,7,8]

**Explanation:** The partition is "ababcbaca", "defegde", "hijhklij". This is a partition so that each letter appears in at most one part. A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits s into less parts.

**Example 2:**

**Input:** s = "eccbbbbdec"

**Output:** [10]

**Constraints:**

*   `1 <= s.length <= 500`
*   `s` consists of lowercase English letters.

## Solution

```erlang
-spec partition_labels(binary()) -> [integer()].
partition_labels(S) when is_binary(S) ->
    Letters = binary_to_list(S),
    % Create an array to store the last position of each letter
    LastPos = find_last_positions(Letters, array:new(26, {default, -1})),
    % Partition the string
    create_partitions(Letters, LastPos, 0, 0, -1, []).

% Helper function to find the last position of each letter
find_last_positions(Letters, Position) ->
    find_last_positions(Letters, Position, 0).
find_last_positions([], Position, _) ->
    Position;
find_last_positions([Letter | Rest], Position, Index) ->
    UpdatedPosition = array:set(Letter - $a, Index, Position),
    find_last_positions(Rest, UpdatedPosition, Index + 1).

% Function to create partitions
create_partitions([], _, _, _, Prev, Result) ->
    lists:reverse(Result);
create_partitions([Letter | Rest], LastPos, Index, Max, Prev, Result) ->
    CurrentMax = array:get(Letter - $a, LastPos),
    NewMax = max(Max, CurrentMax),
    case Index of
        NewMax ->
            NewResult = [Index - Prev | Result],
            create_partitions(Rest, LastPos, Index + 1, 0, Index, NewResult);
        _ ->
            create_partitions(Rest, LastPos, Index + 1, NewMax, Prev, Result)
    end.

% Utility function for finding the maximum of two numbers
max(A, B) when A >= B -> A;
max(_, B) -> B.
```