[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 46\. Permutations

Medium

Given an array `nums` of distinct integers, return _all the possible permutations_. You can return the answer in **any order**.

**Example 1:**

**Input:** nums = [1,2,3]

**Output:** [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]] 

**Example 2:**

**Input:** nums = [0,1]

**Output:** [[0,1],[1,0]] 

**Example 3:**

**Input:** nums = [1]

**Output:** [[1]] 

**Constraints:**

*   `1 <= nums.length <= 6`
*   `-10 <= nums[i] <= 10`
*   All the integers of `nums` are **unique**.



## Solution

```cpp
#include <vector>

class Solution {
public:
    std::vector<std::vector<int>> permute(std::vector<int>& nums) {
        if (nums.empty()) {
            return {};
        }
        std::vector<std::vector<int>> finalResult;
        std::vector<int> currResult;
        std::vector<bool> used(nums.size(), false);
        permuteRecur(nums, finalResult, currResult, used);
        return finalResult;
    }

private:
    void permuteRecur(const std::vector<int>& nums, 
                      std::vector<std::vector<int>>& finalResult, 
                      std::vector<int>& currResult, 
                      std::vector<bool>& used) {
        if (currResult.size() == nums.size()) {
            finalResult.push_back(currResult);
            return;
        }
        for (size_t i = 0; i < nums.size(); ++i) {
            if (used[i]) {
                continue;
            }
            currResult.push_back(nums[i]);
            used[i] = true;
            permuteRecur(nums, finalResult, currResult, used);
            used[i] = false;
            currResult.pop_back();
        }
    }
};
```