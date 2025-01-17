[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 128\. Longest Consecutive Sequence

Medium

Given an unsorted array of integers `nums`, return _the length of the longest consecutive elements sequence._

You must write an algorithm that runs in `O(n)` time.

**Example 1:**

**Input:** nums = [100,4,200,1,3,2]

**Output:** 4

**Explanation:** The longest consecutive elements sequence is `[1, 2, 3, 4]`. Therefore its length is 4.

**Example 2:**

**Input:** nums = [0,3,7,2,5,8,4,6,0,1]

**Output:** 9

**Constraints:**

*   <code>0 <= nums.length <= 10<sup>5</sup></code>
*   <code>-10<sup>9</sup> <= nums[i] <= 10<sup>9</sup></code>

## Solution

```erlang
-spec longest_consecutive(Nums :: [integer()]) -> integer().
longest_consecutive(Nums) ->
    Sorted = lists:sort(Nums),
    SeqLens = count_consecutive(Sorted, [1]),
    lists:max(SeqLens).

-spec count_consecutive(Nums :: [integer()], SeqLens :: [integer()]) -> [integer()].
count_consecutive([H1, H2 | Tail], [SeqHead | SeqTail]) ->
    NewLen = case H1 - H2 of
        -1 -> SeqHead + 1; % Consecutive elements
         0 -> SeqHead;     % Same element, do nothing
         _ -> 1            % Not consecutive, reset count
    end,
    count_consecutive([H2 | Tail], [NewLen | [SeqHead | SeqTail]]);
count_consecutive([_], SeqLens) ->
    SeqLens; % End of list with remaining sequence lengths
count_consecutive([], [_]) ->
    [0]. % Single number case
```