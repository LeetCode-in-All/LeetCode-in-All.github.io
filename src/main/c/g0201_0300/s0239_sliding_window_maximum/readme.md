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

Window position Max 

--------------- ----- 

[1 3 -1] -3 5 3 6 7 **3** 

1 [3 -1 -3] 5 3 6 7 **3** 

1 3 [-1 -3 5] 3 6 7 **5** 

1 3 -1 [-3 5 3] 6 7 **5** 

1 3 -1 -3 [5 3 6] 7 **6** 

1 3 -1 -3 5 [3 6 7] **7**

**Example 2:**

**Input:** nums = [1], k = 1

**Output:** [1]

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>5</sup></code>
*   <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>
*   `1 <= k <= nums.length`

## Solution

```c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* maxSlidingWindow(int* nums, int numsSize, int k, int* returnSize) {
    if (k == 1) {
        *returnSize = numsSize;
        return nums;
    }

    int *queue = malloc(sizeof(int) * numsSize);
    int *res = malloc(sizeof(int) * (numsSize - k + 1));
    int rear = -1;
    int qLen = 0;
    int front = 0;
    int i = 0;
    int resCount = 0;

    for (i = 0; i < numsSize; i++) {
        // Remove elements that are out of the window
        while (qLen > 0 && i - queue[front] >= k) {
            front++;
            qLen--;
        }

        // Remove elements from the back of the queue that are less than the current element
        while (qLen > 0 && nums[i] > nums[queue[rear]]) {
            rear--;
            qLen--;
        }

        // Add the current element index to the queue
        queue[++rear] = i;
        qLen++;

        // Once we have a complete window, add the maximum element (from the front of the queue) to the result
        if (i >= k - 1) {
            res[resCount++] = nums[queue[front]];
        }
    }

    *returnSize = resCount;
    return res;
}
```