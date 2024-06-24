[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 84\. Largest Rectangle in Histogram

Hard

Given an array of integers `heights` representing the histogram's bar height where the width of each bar is `1`, return _the area of the largest rectangle in the histogram_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/04/histogram.jpg)

**Input:** heights = [2,1,5,6,2,3]

**Output:** 10

**Explanation:** The above is a histogram where width of each bar is 1. The largest rectangle is shown in the red area, which has an area = 10 units. 

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/01/04/histogram-1.jpg)

**Input:** heights = [2,4]

**Output:** 4 

**Constraints:**

*   <code>1 <= heights.length <= 10<sup>5</sup></code>
*   <code>0 <= heights[i] <= 10<sup>4</sup></code>

## Solution

```cpp
#include <vector>
#include <algorithm>
#include <climits>

class Solution {
public:
    int largestRectangleArea(std::vector<int>& heights) {
        return largestArea(heights, 0, heights.size());
    }

private:
    int largestArea(const std::vector<int>& a, int start, int limit) {
        if (a.empty()) {
            return 0;
        }
        if (start == limit) {
            return 0;
        }
        if (limit - start == 1) {
            return a[start];
        }
        if (limit - start == 2) {
            int maxOfTwoBars = std::max(a[start], a[start + 1]);
            int areaFromTwo = std::min(a[start], a[start + 1]) * 2;
            return std::max(maxOfTwoBars, areaFromTwo);
        }
        if (checkIfSorted(a, start, limit)) {
            int maxWhenSorted = 0;
            for (int i = start; i < limit; i++) {
                if (a[i] * (limit - i) > maxWhenSorted) {
                    maxWhenSorted = a[i] * (limit - i);
                }
            }
            return maxWhenSorted;
        } else {
            int minInd = findMinInArray(a, start, limit);
            return maxOfThreeNums(
                largestArea(a, start, minInd),
                a[minInd] * (limit - start),
                largestArea(a, minInd + 1, limit)
            );
        }
    }

    int findMinInArray(const std::vector<int>& a, int start, int limit) {
        int min = INT_MAX;
        int minIndex = -1;
        for (int index = start; index < limit; index++) {
            if (a[index] < min) {
                min = a[index];
                minIndex = index;
            }
        }
        return minIndex;
    }

    bool checkIfSorted(const std::vector<int>& a, int start, int limit) {
        for (int i = start + 1; i < limit; i++) {
            if (a[i] < a[i - 1]) {
                return false;
            }
        }
        return true;
    }

    int maxOfThreeNums(int a, int b, int c) {
        return std::max(std::max(a, b), c);
    }
};
```