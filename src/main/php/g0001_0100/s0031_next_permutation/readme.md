[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 31\. Next Permutation

Medium

Implement **next permutation**, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such an arrangement is not possible, it must rearrange it as the lowest possible order (i.e., sorted in ascending order).

The replacement must be **[in place](http://en.wikipedia.org/wiki/In-place_algorithm)** and use only constant extra memory.

**Example 1:**

**Input:** nums = [1,2,3]

**Output:** [1,3,2] 

**Example 2:**

**Input:** nums = [3,2,1]

**Output:** [1,2,3] 

**Example 3:**

**Input:** nums = [1,1,5]

**Output:** [1,5,1] 

**Example 4:**

**Input:** nums = [1]

**Output:** [1] 

**Constraints:**

*   `1 <= nums.length <= 100`
*   `0 <= nums[i] <= 100`

## Solution

```php
class Solution {
    /**
     * @param Integer[] $nums
     * @return NULL
     */
    public function nextPermutation(&$nums) {
        if ($nums == null || count($nums) <= 1) {
            return;
        }
        $i = count($nums) - 2;
        while ($i >= 0 && $nums[$i] >= $nums[$i + 1]) {
            $i--;
        }
        if ($i >= 0) {
            $j = count($nums) - 1;
            while ($nums[$j] <= $nums[$i]) {
                $j--;
            }
            $this->swap($nums, $i, $j);
        }
        $this->reverse($nums, $i + 1, count($nums) - 1);
    }

    private function swap(&$nums, $i, $j) {
        $temp = $nums[$i];
        $nums[$i] = $nums[$j];
        $nums[$j] = $temp;
    }

    private function reverse(&$nums, $i, $j) {
        while ($i < $j) {
            $this->swap($nums, $i++, $j--);
        }
    }
}
```