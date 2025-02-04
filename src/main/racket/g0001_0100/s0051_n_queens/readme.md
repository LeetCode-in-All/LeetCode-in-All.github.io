[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 51\. N-Queens

Hard

The **n-queens** puzzle is the problem of placing `n` queens on an `n x n` chessboard such that no two queens attack each other.

Given an integer `n`, return _all distinct solutions to the **n-queens puzzle**_. You may return the answer in **any order**.

Each solution contains a distinct board configuration of the n-queens' placement, where `'Q'` and `'.'` both indicate a queen and an empty space, respectively.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/13/queens.jpg)

**Input:** n = 4

**Output:** [[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]

**Explanation:** There exist two distinct solutions to the 4-queens puzzle as shown above

**Example 2:**

**Input:** n = 1

**Output:** [["Q"]]

**Constraints:**

*   `1 <= n <= 9`

## Solution

```racket
(define (reverse sequence)
    (foldr (lambda (x y) (append y (list x))) `() sequence))

(define (accumulate op initial sequence)
    (if (null? sequence)
        initial
        (op (car sequence)
            (accumulate op initial (cdr sequence)))))

(define (enumerate-interval low high)
    (if (> low high)
        `()
        (cons low (enumerate-interval (+ low 1) high))))

(define (flatmap proc seq)
    (accumulate append `() (map proc seq)))

(define (queens board-size)
    (define (queen-cols k)
        (if (= k 0)
            (list empty-board)
            (filter
                (lambda (positions) (safe? k positions))
                (flatmap
                    (lambda (rest-of-queens)
                        (map (lambda (new-row)
                            (adjoin-position new-row k rest-of-queens))
                        (enumerate-interval 1 board-size)))
                    (queen-cols (- k 1))))))
    (queen-cols board-size))

(define (adjoin-position new-row k rest-of-queens)
    (append rest-of-queens (list (cons new-row k))))

(define empty-board `())

(define (all proc items)
    (define (iter items)
        (cond ((null? items) #t)
            ((proc (car items)) (iter (cdr items))) 
            (else #f)))
    (iter items))

; None in row, and none in either diagonal
(define (safe? k positions)
    (define (safe-combo? a b)
        (not (or (= (car a) (car b))
                (= (abs (- (car a) (car b)))
                    (abs (- (cdr a) (cdr b)))))))
    (all (lambda (p) (safe-combo? (car (reverse positions)) p)) (cdr (reverse positions))))

; board building to bridge solution to LC format
(define (cdr-by-car lst)
  (map cdr (sort lst >= #:key car)))

(define (solution-to-board n soln)
  (map (lambda (row) (make-row row n)) (cdr-by-car soln)))

(define (make-row k n)
  (string-join (list (k-dots (- k 1)) "Q" (k-dots (- n k))) ""))

(define (k-dots k)
  (string-join (make-list k ".") ""))

(define/contract (solve-n-queens n)
  (-> exact-integer? (listof (listof string?)))
    (map (lambda (soln) (solution-to-board n soln)) (queens n))
  )
```