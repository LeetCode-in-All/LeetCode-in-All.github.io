[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 84\. Largest Rectangle in Histogram

Hard

Given an array of integers `heights` representing the histogram's bar height where the width of each bar is `1`, return _the area of the largest rectangle in the histogram_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/04/histogram.jpg)

**Input:** heights = [2,1,5,6,2,3]

**Output:** 10

**Explanation:** The above is a histogram where width of each bar is 1. 

The largest rectangle is shown in the red area, which has an area = 10 units.

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/01/04/histogram-1.jpg)

**Input:** heights = [2,4]

**Output:** 4

**Constraints:**

*   <code>1 <= heights.length <= 10<sup>5</sup></code>
*   <code>0 <= heights[i] <= 10<sup>4</sup></code>

## Solution

```rust
impl Solution {
    pub fn largest_rectangle_area(heights: Vec<i32>) -> i32 {
        Self::largest_area(&heights, 0, heights.len())
    }

    fn largest_area(heights: &[i32], start: usize, limit: usize) -> i32 {
        if heights.is_empty() || start == limit {
            return 0;
        }
        if limit - start == 1 {
            return heights[start];
        }
        if limit - start == 2 {
            let max_of_two_bars = heights[start].max(heights[start + 1]);
            let area_from_two = heights[start].min(heights[start + 1]) * 2;
            return max_of_two_bars.max(area_from_two);
        }
        if Self::check_if_sorted(heights, start, limit) {
            let mut max_when_sorted = 0;
            for i in start..limit {
                max_when_sorted = max_when_sorted.max(heights[i] * (limit - i) as i32);
            }
            return max_when_sorted;
        } else {
            let min_ind = Self::find_min_in_array(heights, start, limit);
            return Self::max_of_three_nums(
                Self::largest_area(heights, start, min_ind),
                heights[min_ind] * (limit - start) as i32,
                Self::largest_area(heights, min_ind + 1, limit),
            );
        }
    }

    fn find_min_in_array(heights: &[i32], start: usize, limit: usize) -> usize {
        let mut min = i32::MAX;
        let mut min_index = 0;
        for i in start..limit {
            if heights[i] < min {
                min = heights[i];
                min_index = i;
            }
        }
        min_index
    }

    fn check_if_sorted(heights: &[i32], start: usize, limit: usize) -> bool {
        for i in start + 1..limit {
            if heights[i] < heights[i - 1] {
                return false;
            }
        }
        true
    }

    fn max_of_three_nums(a: i32, b: i32, c: i32) -> i32 {
        a.max(b).max(c)
    }
}
```