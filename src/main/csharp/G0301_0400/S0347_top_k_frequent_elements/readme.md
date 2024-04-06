[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 347\. Top K Frequent Elements

Medium

Given an integer array `nums` and an integer `k`, return _the_ `k` _most frequent elements_. You may return the answer in **any order**.

**Example 1:**

**Input:** nums = [1,1,1,2,2,3], k = 2

**Output:** [1,2]

**Example 2:**

**Input:** nums = [1], k = 1

**Output:** [1]

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>5</sup></code>
*   `k` is in the range `[1, the number of unique elements in the array]`.
*   It is **guaranteed** that the answer is **unique**.

**Follow up:** Your algorithm's time complexity must be better than `O(n log n)`, where n is the array's size.

## Solution

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

public class Solution {
    public int[] TopKFrequent(int[] nums, int k) {
        if (k == nums.Length) {
            return nums;
        } 
        //1. build dictionary
        Dictionary<int, int> dict = new Dictionary<int, int>();
        for(int i=0; i < nums.Length; i++) {
            if (!dict.ContainsKey(nums[i])) {
                dict.Add(nums[i],0);
            }  
            dict[nums[i]] +=1;
        }
        //2. build priority queue based on highest to lowest frequency
        PriorityQueue<int, int> pq = new PriorityQueue<int, int>(Comparer<int>.Create((x, y) => y.CompareTo(x)));
        foreach (var key in dict.Keys) {
            pq.Enqueue(key, dict[key]);
        }
        // 3. return top k elements from Priority Queue
        var result = new int[k];
        for (var i = 0; i < k; i++) {
            result[i] = pq.Dequeue();
        }
        return result;
    }
}
```