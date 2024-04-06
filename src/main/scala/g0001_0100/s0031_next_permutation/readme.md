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

```scala
object Solution {
    def nextPermutation(nums: Array[Int]): Unit = {
        if (nums == null || nums.length <= 1) {
            return
        }
        var i = nums.length - 2
        while (i >= 0 && nums(i) >= nums(i + 1)) {
            i -= 1
        }
        if (i >= 0) {
            var j = nums.length - 1
            while (nums(j) <= nums(i)) {
                j -= 1
            }
            swap(nums, i, j)
        }
        reverse(nums, i + 1, nums.length - 1)
    }

    private def swap(nums: Array[Int], i: Int, j: Int): Unit = {
        val temp = nums(i)
        nums(i) = nums(j)
        nums(j) = temp
    }

    private def reverse(nums: Array[Int], i: Int, j: Int): Unit = {
        var start = i
        var end = j
        while (start < end) {
            swap(nums, start, end)
            start += 1
            end -= 1
        }
    }
}
```