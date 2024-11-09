[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 4\. Median of Two Sorted Arrays

Hard

Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return **the median** of the two sorted arrays.

The overall run time complexity should be `O(log (m+n))`.

**Example 1:**

**Input:** nums1 = [1,3], nums2 = [2]

**Output:** 2.00000

**Explanation:** merged array = [1,2,3] and median is 2. 

**Example 2:**

**Input:** nums1 = [1,2], nums2 = [3,4]

**Output:** 2.50000

**Explanation:** merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5. 

**Example 3:**

**Input:** nums1 = [0,0], nums2 = [0,0]

**Output:** 0.00000 

**Example 4:**

**Input:** nums1 = [], nums2 = [1]

**Output:** 1.00000 

**Example 5:**

**Input:** nums1 = [2], nums2 = []

**Output:** 2.00000 

**Constraints:**

*   `nums1.length == m`
*   `nums2.length == n`
*   `0 <= m <= 1000`
*   `0 <= n <= 1000`
*   `1 <= m + n <= 2000`
*   <code>-10<sup>6</sup> <= nums1[i], nums2[i] <= 10<sup>6</sup></code>

## Solution

```c
#include <stdio.h>
#include <limits.h>

double findMedianSortedArrays(int* nums1, int n1, int* nums2, int n2) {
    if (n1 > n2) {
        return findMedianSortedArrays(nums2, n2, nums1, n1);
    }

    int low = 0, high = n1;
    while (low <= high) {
        int cut1 = (low + high) / 2;
        int cut2 = (n1 + n2 + 1) / 2 - cut1;

        int l1 = (cut1 == 0) ? INT_MIN : nums1[cut1 - 1];
        int l2 = (cut2 == 0) ? INT_MIN : nums2[cut2 - 1];
        int r1 = (cut1 == n1) ? INT_MAX : nums1[cut1];
        int r2 = (cut2 == n2) ? INT_MAX : nums2[cut2];

        if (l1 <= r2 && l2 <= r1) {
            if ((n1 + n2) % 2 == 0) {
                return (double)(fmax(l1, l2) + fmin(r1, r2)) / 2.0;
            } else {
                return (double)fmax(l1, l2);
            }
        } else if (l1 > r2) {
            high = cut1 - 1;
        } else {
            low = cut1 + 1;
        }
    }

    return 0.0;
}
```