[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 239\. Sliding Window Maximum

Hard

You are given an array of integers `nums`, there is a sliding window of size `k` which is moving from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position.

Return _the max sliding window_.

**Example 1:**

**Input:** nums = [1,3,-1,-3,5,3,6,7], k = 3

**Output:** [3,3,5,5,6,7]

**Explanation:**

    Window position        Max
    ---------------       -----
    [1 3 -1] -3 5 3 6 7     3
    1 [3 -1 -3] 5 3 6 7     3
    1 3 [-1 -3 5] 3 6 7     5
    1 3 -1 [-3 5 3] 6 7     5
    1 3 -1 -3 [5 3 6] 7     6
    1 3 -1 -3 5 [3 6 7]     7 

**Example 2:**

**Input:** nums = [1], k = 1

**Output:** [1] 

**Example 3:**

**Input:** nums = [1,-1], k = 1

**Output:** [1,-1] 

**Example 4:**

**Input:** nums = [9,11], k = 2

**Output:** [11] 

**Example 5:**

**Input:** nums = [4,-2], k = 2

**Output:** [4] 

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>5</sup></code>
*   <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>
*   `1 <= k <= nums.length`

## Solution

```swift
import Collections

class Solution {
    func maxSlidingWindow(_ nums: [Int], _ k: Int) -> [Int]
    {
        // monontonic decreasing queue, storing indexes of nums        
        var queue = Deque<Int>() 
        var ans: [Int] = []
        for i in 0..<nums.count
        {
            // mantain window size no bigger then k
            while !queue.isEmpty && i - queue.first! >= k {
                queue.removeFirst()
            }
            
            // mantain queue monotonic decreasing
            while !queue.isEmpty && nums[queue.last!] < nums[i] {
                queue.removeLast()
            }
            queue.append(i)
            
            if i >= k-1 {
                ans.append(nums[queue.first!]) // max value in window
            }
        }
        return ans
    }
}
```