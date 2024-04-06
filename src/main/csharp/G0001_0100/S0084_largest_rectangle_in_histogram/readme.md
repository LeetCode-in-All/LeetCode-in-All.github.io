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

```csharp
public class Solution {
    public int LargestRectangleArea(int[] heights) {
        int maxArea = 0, i = 0;
        Stack<int> stack = new Stack<int>();
        while (i <= heights.Length) {
            var currHeight = i == heights.Length ? 0 : heights[i];
            if (!stack.Any() || currHeight >= heights[stack.Peek()]) {
                stack.Push(i);
                i++;
            }
            else {
                int index = stack.Pop();
                int height = heights[index];
                int width = (!stack.Any()) ? i : (i - 1) - stack.Peek();
                maxArea = Math.Max(maxArea, height * width);
            }
        }
        return maxArea;
    }
}
```