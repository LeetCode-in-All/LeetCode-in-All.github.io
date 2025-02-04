[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 62\. Unique Paths

Medium

There is a robot on an `m x n` grid. The robot is initially located at the **top-left corner** (i.e., `grid[0][0]`). The robot tries to move to the **bottom-right corner** (i.e., `grid[m - 1][n - 1]`). The robot can only move either down or right at any point in time.

Given the two integers `m` and `n`, return _the number of possible unique paths that the robot can take to reach the bottom-right corner_.

The test cases are generated so that the answer will be less than or equal to <code>2 * 10<sup>9</sup></code>.

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)

**Input:** m = 3, n = 7

**Output:** 28

**Example 2:**

**Input:** m = 3, n = 2

**Output:** 3

**Explanation:** From the top-left corner, there are a total of 3 ways to reach the bottom-right corner: 

1. Right -> Down -> Down 

2. Down -> Down -> Right 

3. Down -> Right -> Down

**Constraints:**

*   `1 <= m, n <= 100`

## Solution

```racket
(define (calc-path! start end direction cache other-p)
  (begin (if (string=? direction "v")
      (for ([i (in-range start end)])
        (if (= other-p 0)
            (hash-set! cache (list 0 i) 1)
            (hash-set! cache
                       (list other-p i)
                       (+ (hash-ref cache (list (- other-p 1) i))
                          (hash-ref cache (list other-p (- i 1)))))))
      (for ([i (in-range start end)])
        (if (= other-p 0)
            (hash-set! cache (list i 0) 1)
            (hash-set! cache (list i other-p)
                       (+ (hash-ref cache (list i (- other-p 1)))
                          (hash-ref cache (list (- i 1) other-p)))))))
         cache))

(define (dp-path x y target-x target-y cache)
  (if (and (>= x target-x) (>= y target-y))
      (hash-ref cache (list (- target-x 1) (- target-y 1)))
      (let* ([cache
              (begin
                (when (<= x target-x) (calc-path! x (add1 target-x) "h" cache y))
                (when (<= y target-x) (calc-path! y (add1 target-y) "v" cache x))
                cache)]
             [x (if (< x target-x) (add1 x) x)]
             [y (if (< y target-y) (add1 y) y)])
        (dp-path x y target-x target-y cache))))

(define (start-dp target-x target-y)
 (dp-path 0 0 target-x target-y (make-hash)))


(define/contract (unique-paths m n)
  (-> exact-integer? exact-integer? exact-integer?)
  (start-dp m n))
```