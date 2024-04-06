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

```ruby
# @param {Integer[]} heights
# @return {Integer}
def largest_rectangle_area(heights)
  area = 0
  stack = []
  return 0 if heights.empty?
  return heights[0] * heights.length if heights.uniq.length == 1

  heights.each.with_index do |height, index|
    start = index
    while !stack.empty? && stack.last[1] > height do
      i, h = stack.pop
      area = [area, h * (index - i)].max
      start = i
    end
    stack << [start, height]
  end

  stack.each do |i, s|
    area = [area, s * (heights.length - i)].max
  end

  area
end
```