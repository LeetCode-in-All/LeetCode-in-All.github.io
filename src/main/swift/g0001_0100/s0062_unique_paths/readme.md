[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 62\. Unique Paths

Medium

A robot is located at the top-left corner of a `m x n` grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)

**Input:** m = 3, n = 7

**Output:** 28 

**Example 2:**

**Input:** m = 3, n = 2

**Output:** 3

**Explanation:**

    From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
    1. Right -> Down -> Down
    2. Down -> Down -> Right
    3. Down -> Right -> Down 

**Example 3:**

**Input:** m = 7, n = 3

**Output:** 28 

**Example 4:**

**Input:** m = 3, n = 3

**Output:** 6 

**Constraints:**

*   `1 <= m, n <= 100`
*   It's guaranteed that the answer will be less than or equal to <code>2 * 10<sup>9</sup></code>.

To solve the "Unique Paths" problem in Swift with the Solution class, follow these steps:

1. Define a method `uniquePaths` in the `Solution` class that takes two integers `m` and `n` as input and returns the number of unique paths from the top-left corner to the bottom-right corner of an `m x n` grid.
2. Initialize a 2D array `dp` of size `m x n` to store the number of unique paths for each position in the grid.
3. Initialize the first row and first column of `dp` to 1 since there is only one way to reach any position in the first row or column (by moving only right or down).
4. Iterate over each position `(i, j)` in the grid, starting from the second row and second column:
   - Update `dp[i][j]` by adding the number of unique paths from the cell above `(i-1, j)` and the cell to the left `(i, j-1)`.
5. Return the value of `dp[m-1][n-1]`, which represents the number of unique paths to reach the bottom-right corner of the grid.

Here's the implementation of the `uniquePaths` method in Swift:

```swift
public class Solution {
    public func uniquePaths(_ m: Int, _ n: Int) -> Int {
        var dp = Array(repeating: Array(repeating: 0, count: n), count: m)
        
        for i in 0..<m {
            dp[i][0] = 1
        }
        
        for j in 0..<n {
            dp[0][j] = 1
        }
        
        for i in 1..<m {
            for j in 1..<n {
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1]
            }
        }
        
        return dp[m - 1][n - 1]
    }
}
```

This implementation efficiently calculates the number of unique paths using dynamic programming, with a time complexity of O(m * n) and a space complexity of O(m * n).