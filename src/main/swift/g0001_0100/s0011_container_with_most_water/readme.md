[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 11\. Container With Most Water

Medium

Given `n` non-negative integers <code>a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub></code> , where each represents a point at coordinate <code>(i, a<sub>i</sub>)</code>. `n` vertical lines are drawn such that the two endpoints of the line `i` is at <code>(i, a<sub>i</sub>)</code> and `(i, 0)`. Find two lines, which, together with the x-axis forms a container, such that the container contains the most water.

**Notice** that you may not slant the container.

**Example 1:**

![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

**Input:** height = [1,8,6,2,5,4,8,3,7]

**Output:** 49

**Explanation:** The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49. 

**Example 2:**

**Input:** height = [1,1]

**Output:** 1 

**Example 3:**

**Input:** height = [4,3,2,1,4]

**Output:** 16 

**Example 4:**

**Input:** height = [1,2,1]

**Output:** 2 

**Constraints:**

*   `n == height.length`
*   <code>2 <= n <= 10<sup>5</sup></code>
*   <code>0 <= height[i] <= 10<sup>4</sup></code>

To solve the Container With Most Water problem in Swift using a `Solution` class, we'll follow these steps:

1. Define a `Solution` class with a method named `maxArea` that takes an array of integers `height` as input and returns the maximum area of water that can be contained.
2. Initialize two pointers, `left` pointing to the start of the array and `right` pointing to the end of the array.
3. Initialize a variable `maxArea` to store the maximum area encountered so far, initially set to 0.
4. Iterate while `left` is less than `right`.
5. Calculate the current area using the formula: `(right - left) * min(height[left], height[right])`.
6. Update `maxArea` if the current area is greater than `maxArea`.
7. Move the pointer pointing to the smaller height towards the other pointer. If `height[left] < height[right]`, increment `left`, otherwise decrement `right`.
8. Continue the iteration until `left` becomes greater than or equal to `right`.
9. Return `maxArea`.

Here's the implementation:

```swift
class Solution {
    func maxArea(_ height: [Int]) -> Int {
        var i = 0
        var j = height.count - 1
        var mx = Int.min
        // Base condition
        guard height.count != 2 else {
            return min(height[0], height[1])
        }

        // Hypothesis
    
        // Induction
        while (j > i) {
            let dis = j - i
            var area = height[i] * dis
            if height[i] < height[j] {
                i += 1
            } else {
                area = height[j] * dis
                j -= 1
            }
            mx = max(mx, area)
        }
         return mx
    }
}
```

This implementation provides a solution to the Container With Most Water problem in Swift.