[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 55\. Jump Game

Medium

You are given an integer array `nums`. You are initially positioned at the array's **first index**, and each element in the array represents your maximum jump length at that position.

Return `true` _if you can reach the last index, or_ `false` _otherwise_.

**Example 1:**

**Input:** nums = [2,3,1,1,4]

**Output:** true

**Explanation:** Jump 1 step from index 0 to 1, then 3 steps to the last index. 

**Example 2:**

**Input:** nums = [3,2,1,0,4]

**Output:** false

**Explanation:** You will always arrive at index 3 no matter what. Its maximum jump length is 0, which makes it impossible to reach the last index. 

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>4</sup></code>
*   <code>0 <= nums[i] <= 10<sup>5</sup></code>

## Solution

```ruby
# @param {Integer[]} nums
# @return {Boolean}
def can_jump(nums)
  sz = nums.length
  # We set 1 so it won't break on the first iteration
  tmp = 1

  (0...sz).each do |i|
    # We always deduct tmp for every iteration
    tmp -= 1
    return false if tmp < 0

    # Get the maximum value because this value is supposed
    # to be our iterator. If both values are 0, then the next
    # iteration we will return false.
    # We can stop the whole iteration with this condition. Without this condition, the code
    # runs in 2ms (79.6%). Adding this condition improves the performance to 1ms (100%)
    # because if the test case jump value is quite large, instead of just iterating, we can
    # just check using this condition.
    # Example: [10, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0] -> we can just jump to the end without
    # iterating the whole array.
    tmp = [tmp, nums[i]].max
    return true if i + tmp >= sz - 1
  end

  # We can just return true at the end because if tmp is 0 on the previous
  # iteration,
  # even though the next iteration index is the last one, it will return false under the
  # tmp < 0 condition.
  true
end
```