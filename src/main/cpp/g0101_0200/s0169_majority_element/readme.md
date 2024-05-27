[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 169\. Majority Element

Easy

Given an array `nums` of size `n`, return _the majority element_.

The majority element is the element that appears more than `⌊n / 2⌋` times. You may assume that the majority element always exists in the array.

**Example 1:**

**Input:** nums = [3,2,3]

**Output:** 3 

**Example 2:**

**Input:** nums = [2,2,1,1,1,2,2]

**Output:** 2 

**Constraints:**

*   `n == nums.length`
*   <code>1 <= n <= 5 * 10<sup>4</sup></code>
*   <code>-2<sup>31</sup> <= nums[i] <= 2<sup>31</sup> - 1</code>

**Follow-up:** Could you solve the problem in linear time and in `O(1)` space?

## Solution

```cpp
#include <vector>
using namespace std;

class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int count = 1;
        int majority = nums[0];

        // For Potential Majority Element
        for (size_t i = 1; i < nums.size(); i++) {
            if (nums[i] == majority) {
                count++;
            } else {
                if (count > 1) {
                    count--;
                } else {
                    majority = nums[i];
                }
            }
        }

        // For Confirmation
        count = 0;
        for (int num : nums) {
            if (num == majority) {
                count++;
            }
        }

        if (count >= (nums.size() / 2) + 1) {
            return majority;
        } else {
            return -1;
        }
    }
};
```