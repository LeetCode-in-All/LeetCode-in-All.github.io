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

```php
class Solution {
    /**
     * @param Integer[] $heights
     * @return Integer
     */
    public function largestRectangleArea($heights) {
        return $this->largestArea($heights, 0, count($heights));
    }

    private function largestArea($a, $start, $limit) {
        if ($a == null || empty($a)) {
            return 0;
        }
        if ($start == $limit) {
            return 0;
        }
        if ($limit - $start == 1) {
            return $a[$start];
        }
        if ($limit - $start == 2) {
            $maxOfTwoBars = max($a[$start], $a[$start + 1]);
            $areaFromTwo = min($a[$start], $a[$start + 1]) * 2;
            return max($maxOfTwoBars, $areaFromTwo);
        }
        if ($this->checkIfSorted($a, $start, $limit)) {
            $maxWhenSorted = 0;
            for ($i = $start; $i < $limit; $i++) {
                if ($a[$i] * ($limit - $i) > $maxWhenSorted) {
                    $maxWhenSorted = $a[$i] * ($limit - $i);
                }
            }
            return $maxWhenSorted;
        } else {
            $minInd = $this->findMinInArray($a, $start, $limit);
            return $this->maxOfThreeNums(
                $this->largestArea($a, $start, $minInd),
                $a[$minInd] * ($limit - $start),
                $this->largestArea($a, $minInd + 1, $limit));
        }
    }

    private function findMinInArray($a, $start, $limit) {
        $min = PHP_INT_MAX;
        $minIndex = -1;
        for ($index = $start; $index < $limit; $index++) {
            if ($a[$index] < $min) {
                $min = $a[$index];
                $minIndex = $index;
            }
        }
        return $minIndex;
    }

    private function checkIfSorted($a, $start, $limit) {
        for ($i = $start + 1; $i < $limit; $i++) {
            if ($a[$i] < $a[$i - 1]) {
                return false;
            }
        }
        return true;
    }

    private function maxOfThreeNums($a, $b, $c) {
        return max(max($a, $b), $c);
    }
}
```