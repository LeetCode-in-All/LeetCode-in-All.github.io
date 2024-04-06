[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 7\. Reverse Integer

Medium

Given a signed 32-bit integer `x`, return `x` _with its digits reversed_. If reversing `x` causes the value to go outside the signed 32-bit integer range <code>[-2<sup>31</sup>, 2<sup>31</sup> - 1]</code>, then return `0`.

**Assume the environment does not allow you to store 64-bit integers (signed or unsigned).**

**Example 1:**

**Input:** x = 123

**Output:** 321 

**Example 2:**

**Input:** x = -123

**Output:** -321 

**Example 3:**

**Input:** x = 120

**Output:** 21 

**Example 4:**

**Input:** x = 0

**Output:** 0 

**Constraints:**

*   <code>-2<sup>31</sup> <= x <= 2<sup>31</sup> - 1</code>

## Solution

```typescript
function reverse(x: number): number {
    let remaining = Math.abs(x)
    let power = Math.floor(Math.log10(remaining))
    let reversed = 0
    while (remaining > 0) {
        const digit = remaining % 10
        remaining = (remaining - digit) / 10
        reversed += digit * 10 ** power--
        if (reversed > 2 ** 31 - 1) return 0
    }
    return x > 0 ? reversed : -reversed
}

export { reverse }
```