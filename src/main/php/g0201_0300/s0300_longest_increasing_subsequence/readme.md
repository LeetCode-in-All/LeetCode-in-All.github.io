[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 300\. Longest Increasing Subsequence

Medium

Given an integer array `nums`, return the length of the longest strictly increasing subsequence.

A **subsequence** is a sequence that can be derived from an array by deleting some or no elements without changing the order of the remaining elements. For example, `[3,6,2,7]` is a subsequence of the array `[0,3,1,6,2,2,7]`.

**Example 1:**

**Input:** nums = [10,9,2,5,3,7,101,18]

**Output:** 4

**Explanation:** The longest increasing subsequence is [2,3,7,101], therefore the length is 4. 

**Example 2:**

**Input:** nums = [0,1,0,3,2,3]

**Output:** 4 

**Example 3:**

**Input:** nums = [7,7,7,7,7,7,7]

**Output:** 1 

**Constraints:**

*   `1 <= nums.length <= 2500`
*   <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>

**Follow up:** Can you come up with an algorithm that runs in `O(n log(n))` time complexity?

## Solution

```php
class Solution {
    /**
     * @param Integer[] $nums
     * @return Integer
     */
    public function lengthOfLIS($nums) {
        if ($nums == null || count($nums) == 0) {
            return 0;
        }
        $dp = array_fill(0, count($nums) + 1, PHP_INT_MAX);
        // prefill the dp table
        for ($i = 1; $i < count($dp); $i++) {
            $dp[$i] = PHP_INT_MAX;
        }
        $left = 1;
        $right = 1;
        foreach ($nums as $curr) {
            $start = $left;
            $end = $right;
            // binary search, find the one that is lower than curr
            while ($start + 1 < $end) {
                $mid = $start + (int)(($end - $start) / 2);
                if ($dp[$mid] > $curr) {
                    $end = $mid;
                } else {
                    $start = $mid;
                }
            }
            // update our dp table
            if ($dp[$start] > $curr) {
                $dp[$start] = $curr;
            } elseif ($curr > $dp[$start] && $curr < $dp[$end]) {
                $dp[$end] = $curr;
            } elseif ($curr > $dp[$end]) {
                $dp[++$end] = $curr;
                $right++;
            }
        }
        return $right;
    }
}
```