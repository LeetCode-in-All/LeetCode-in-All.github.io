[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 42\. Trapping Rain Water

Hard

Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)

**Input:** height = [0,1,0,2,1,0,1,3,2,1,2,1]

**Output:** 6

**Explanation:** The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped. 

**Example 2:**

**Input:** height = [4,2,0,3,2,5]

**Output:** 9 

**Constraints:**

*   `n == height.length`
*   <code>1 <= n <= 2 * 10<sup>4</sup></code>
*   <code>0 <= height[i] <= 10<sup>5</sup></code>

## Solution

```php
class Solution {
    /**
     * @param Integer[] $height
     * @return Integer
     */
    public function trap($height) {
        $result = 0;
        $i = 0;
        $j = count($height) - 1;
        $maxLeft = 0;
        $maxRight = 0;
        while ($i < $j) {
            if ($height[$i] < $height[$j]) {
                $maxLeft = max($maxLeft, $height[$i]);
                $result += $maxLeft - $height[$i];
                $i++;
            } else {
                $maxRight = max($maxRight, $height[$j]);
                $result += $maxRight - $height[$j];
                $j--;
            }
        }
        return $result;
    }
}
```