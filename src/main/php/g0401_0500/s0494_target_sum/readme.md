[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 494\. Target Sum

Medium

You are given an integer array `nums` and an integer `target`.

You want to build an **expression** out of nums by adding one of the symbols `'+'` and `'-'` before each integer in nums and then concatenate all the integers.

*   For example, if `nums = [2, 1]`, you can add a `'+'` before `2` and a `'-'` before `1` and concatenate them to build the expression `"+2-1"`.

Return the number of different **expressions** that you can build, which evaluates to `target`.

**Example 1:**

**Input:** nums = [1,1,1,1,1], target = 3

**Output:** 5

**Explanation:**

    There are 5 ways to assign symbols to make the sum of nums be target 3.
    -1 + 1 + 1 + 1 + 1 = 3
    +1 - 1 + 1 + 1 + 1 = 3
    +1 + 1 - 1 + 1 + 1 = 3
    +1 + 1 + 1 - 1 + 1 = 3
    +1 + 1 + 1 + 1 - 1 = 3 

**Example 2:**

**Input:** nums = [1], target = 1

**Output:** 1 

**Constraints:**

*   `1 <= nums.length <= 20`
*   `0 <= nums[i] <= 1000`
*   `0 <= sum(nums[i]) <= 1000`
*   `-1000 <= target <= 1000`

## Solution

```php
class Solution {
    /**
     * @param Integer[] $nums
     * @param Integer $target
     * @return Integer
     */
    public function findTargetSumWays($nums, $s) {
        $sum = 0;
        $s = abs($s);
        foreach ($nums as $num) {
            $sum += $num;
        }
        // Invalid s, just return 0
        if ($s > $sum || ($sum + $s) % 2 != 0) {
            return 0;
        }
        $dp = array_fill(0, ($sum + $s) / 2 + 1, array_fill(0, count($nums) + 1, 0));
        $dp[0][0] = 1;
        // empty knapsack must be processed specially
        for ($i = 0; $i < count($nums); $i++) {
            if ($nums[$i] == 0) {
                $dp[0][$i + 1] = $dp[0][$i] * 2;
            } else {
                $dp[0][$i + 1] = $dp[0][$i];
            }
        }
        for ($i = 1; $i < count($dp); $i++) {
            for ($j = 0; $j < count($nums); $j++) {
                $dp[$i][$j + 1] += $dp[$i][$j];
                if ($nums[$j] <= $i) {
                    $dp[$i][$j + 1] += $dp[$i - $nums[$j]][$j];
                }
            }
        }
        return $dp[($sum + $s) / 2][count($nums)];
    }
}
```