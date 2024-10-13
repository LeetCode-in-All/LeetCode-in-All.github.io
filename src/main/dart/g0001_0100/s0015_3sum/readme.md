[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 15\. 3Sum

Medium

Given an integer array nums, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

**Example 1:**

**Input:** nums = [-1,0,1,2,-1,-4]

**Output:** [[-1,-1,2],[-1,0,1]] 

**Example 2:**

**Input:** nums = []

**Output:** [] 

**Example 3:**

**Input:** nums = [0]

**Output:** [] 

**Constraints:**

*   `0 <= nums.length <= 3000`
*   <code>-10<sup>5</sup> <= nums[i] <= 10<sup>5</sup></code>

## Solution

```dart
class Solution {
  List<List<int>> threeSum(List<int> nums) {
    List<List<int>> result = [];

    if (nums.length < 3) {
      return result; // There can't be triplets if there are less than 3 elements.
    }

    nums.sort(); // Sort the array to make the two-pointer approach easier.

    for (int i = 0; i < nums.length - 2; i++) {
      if (i > 0 && nums[i] == nums[i - 1]) {
        continue; // Skip duplicates for the first element of the triplet.
      }

      int target = -nums[i];
      int left = i + 1;
      int right = nums.length - 1;

      while (left < right) {
        int sum = nums[left] + nums[right];

        if (sum == target) {
          result.add([nums[i], nums[left], nums[right]]);

          while (left < right && nums[left] == nums[left + 1]) {
            left++; // Skip duplicates for the second element of the triplet.
          }

          while (left < right && nums[right] == nums[right - 1]) {
            right--; // Skip duplicates for the third element of the triplet.
          }

          left++;
          right--;
        } else if (sum < target) {
          left++;
        } else {
          right--;
        }
      }
    }

    return result;
  }
}
```