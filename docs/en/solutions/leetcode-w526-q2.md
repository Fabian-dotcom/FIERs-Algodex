---
tags:
  - LeetCode
  - Array
  - Math
  - Number Theory
  - Greedy
  - Medium
---

# LeetCode Weekly 526 Q2: Minimize the Maximum Value of GCD-Connected Array

- **Platform:** Weekly Contest 526, Q2
- **Difficulty:** Medium
- **Categories:** Array, Math, Number Theory, Greedy
- **Related Concepts:** [Bitwise Operations](../glossary/bit-manipulation.md) | [Algebraic One-Pass Optimization](../glossary/algebraic-one-pass.md)

---

## Problem Statement

An array `nums` of length $n$ is called **GCD-Connected** when:

- $\text{nums}[i] > 0$ for all $i$,
- strictly increasing: $\text{nums}[i] < \text{nums}[i+1]$,
- $\text{nums}[\text{index}] = \text{value}$ is fixed,
- $\gcd(\text{nums}[i], \text{nums}[i+1]) > 1$ for every adjacent pair.

Return the **minimum possible maximum** $\text{nums}[n-1]$, or $-1$ if no such array exists.

### Example

```text
Input:  n = 4, index = 2, value = 8
Output: 14
Explanation: e.g. [4, 6, 8, 10] — every adjacent pair shares a factor ≥ 2.
```

---

## Intuition & Solution Approach

### Optimized core idea (smallest-prime-factor chain)

1. **Adjacent values differ by at least 2**, because $\gcd(x, x+1) = 1$ — consecutive integers are always coprime.
2. **For $y > x$ with $\gcd(x, y) = g > 1$**, $g \mid (y - x)$ holds, so the **smallest reachable distance** is $y - x \ge \text{spf}(x)$ (the smallest prime factor of $x$). The minimal growing chain therefore advances in steps of two starting from the smallest prime factor.
3. **Right of `index`:** If `value` is even ($p = 2$), the next $m = n - 1 - \text{index}$ elements follow as `value + 2m`. If `value` is odd with smallest prime factor $p$, first jump to the even `value + p`, then advance in steps of two: $\text{value} + p + 2(m-1)$.
4. **Left of `index`:** The maximum element count including `value` is `value / 2` (even `value`) or $1 + (value - p)/2$ (odd). If `index + 1` exceeds this budget, no valid array exists → $-1$.

The trial-and-error search for the chain length disappears entirely — the answer is a **closed formula** plus an $\mathcal{O}(\sqrt{\text{value}})$ trial division for the smallest prime factor.

---

## Implementation (Python 3)

```python
class Solution:
    def minMax(self, n: int, index: int, value: int) -> int:
        """Determines the minimal maximum of a GCD-connected array.

        Args:
            n: Length of the target array
            index: Fixed position
            value: Fixed value at position index

        Returns:
            Minimal possible nums[n-1], or -1
        """
        if n == 1:
            return value
        if value == 1:
            return -1  # gcd with 1 is never > 1

        # Determine the smallest prime factor of value
        if value & 1 == 0:
            p = 2
        else:
            p = value
            d = 3
            while d * d <= value:
                if value % d == 0:
                    p = d
                    break
                d += 2

        # Maximum element count on the left, including value:
        # even -> 2, 4, ..., value (value/2 elements)
        # odd -> value - p is even, then step down by two
        left = value >> 1 if p == 2 else 1 + ((value - p) >> 1)
        if index + 1 > left:
            return -1

        m = n - 1 - index   # number of elements right of value
        if m == 0:
            return value
        if p == 2:
            return value + 2 * m
        return value + p + 2 * (m - 1)
```

---

## Complexity Analysis

| Dimension                              | Complexity                         | Rationale                                                                             |
| :------------------------------------- | :--------------------------------- | :------------------------------------------------------------------------------------ |
| **[Time](../glossary/o-notation.md)**  | $\mathcal{O}(\sqrt{\text{value}})$ | Trial division for the smallest prime factor; the rest are $\mathcal{O}(1)$ formulas. |
| **[Space](../glossary/o-notation.md)** | $\mathcal{O}(1)$                   | Scalars only.                                                                         |

---

## Edge Cases & Pitfalls

- [x] **`value == 1`:** $\gcd(1, x) = 1$ always → no valid array.
- [x] **$n = 1$:** The array consists of `value` alone; all conditions hold trivially.
- [x] **Odd `value`:** The first right neighbor is `value + p` (an odd multiple of the prime factor), then steps of two — not a blind `+2`.
- [x] **Left budget:** If more positions left of `index` are needed than constructible, the answer is $-1$.
