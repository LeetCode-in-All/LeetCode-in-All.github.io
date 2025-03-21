[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 238\. Product of Array Except Self

Medium

Given an integer array `nums`, return _an array_ `answer` _such that_ `answer[i]` _is equal to the product of all the elements of_ `nums` _except_ `nums[i]`.

The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

You must write an algorithm that runs in `O(n)` time and without using the division operation.

**Example 1:**

**Input:** nums = [1,2,3,4]

**Output:** [24,12,8,6]

**Example 2:**

**Input:** nums = [-1,1,0,-3,3]

**Output:** [0,0,9,0,0]

**Constraints:**

*   <code>2 <= nums.length <= 10<sup>5</sup></code>
*   `-30 <= nums[i] <= 30`
*   The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

**Follow up:** Can you solve the problem in `O(1) `extra space complexity? (The output array **does not** count as extra space for space complexity analysis.)

## Solution

```erlang
-spec product_except_self(Nums :: [integer()]) -> [integer()].
product_except_self(Nums) ->
    Forwards = product(Nums, [], 1),
    Backwards = lists:reverse(product(lists:reverse(Nums), [], 1)),
    except_self([1|Forwards], Backwards ++ [1], []).

product([], Res, _) -> lists:reverse(Res);
product([H|T], Res, Acc) ->
    P = H * Acc,
    product(T, [P|Res], P).

except_self([_], [_], Res) -> lists:reverse(Res);
except_self([F|T1], [_, B|T2], Res) ->
    except_self(T1, [B|T2], [F * B|Res]).
```