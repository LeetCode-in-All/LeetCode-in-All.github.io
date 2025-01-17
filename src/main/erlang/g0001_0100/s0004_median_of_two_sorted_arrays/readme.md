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

```erlang
-spec find_median_sorted_arrays(Nums1 :: [integer()], Nums2 :: [integer()]) -> float().
find_median_sorted_arrays(Nums1, Nums2) -> 
    Len = length(Nums1) + length(Nums2),
    find_median_sorted_arrays(Nums1, Nums2, [], -1, 0, 0, Len rem 2, Len div 2).
find_median_sorted_arrays(_, _, [H|T], Index, _, _, Even, Index) ->
        if Even =:= 1 -> H;
            true -> (H + lists:nth(1, T)) / 2
        end;
find_median_sorted_arrays([], [H2|T2], MyArr, Index, Indx1, Indx2, Even, Middle) ->
    find_median_sorted_arrays([], T2, [H2|MyArr], Index + 1, Indx1, Indx2 + 1, Even, Middle);
find_median_sorted_arrays([H1|T1], [], MyArr, Index, Indx1, Indx2, Even, Middle) ->
    find_median_sorted_arrays(T1, [], [H1|MyArr], Index + 1, Indx1, Indx2 + 1, Even, Middle);
find_median_sorted_arrays([H1|T1], [H2|T2], MyArr, Index, Indx1, Indx2, Even, Middle) when H1 < H2 -> 
    find_median_sorted_arrays(T1, [H2|T2], [H1|MyArr], Index + 1, Indx1 + 1, Indx2, Even, Middle);
find_median_sorted_arrays([H1|T1], [H2|T2], MyArr, Index, Indx1, Indx2, Even, Middle)-> 
    find_median_sorted_arrays([H1|T1], T2, [H2|MyArr], Index + 1, Indx1, Indx2 + 1, Even, Middle).
```