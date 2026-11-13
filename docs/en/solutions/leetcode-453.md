---
tags:
  - LeetCode
  - Array
  - Math
  - Greedy
  - Easy
---

# LeetCode 453: Minimum Moves to Equal Array Elements

- **Platform:** [LeetCode #453](https://leetcode.com/problems/minimum-moves-to-equal-array-elements/)
- **Difficulty:** Easy
- **Categories:** Array, Math, Greedy
- **Related Concepts:** [Algebraic One-Pass Optimization](../glossary/algebraic-one-pass.md) | [Memory-Efficient Generators](../glossary/generator-expressions.md)

---

## Problem Statement

You are given an array `nums` of length $n$. In one move, **$n - 1$ elements** may be incremented by $1$. Return the minimum number of moves until all elements are equal.

### Example

```text
Input:  nums = [1, 2, 3]
Output: 3
Explanation: [1,2,3] → [2,3,3] → [3,4,3] → [3,3,3] (or an equivalent move sequence).
```

---

## Intuition & Solution Approach

### 1. Naive idea

Simulate the moves directly, incrementing the $n-1$ smallest elements each time.

- Correct, but $\mathcal{O}(n \cdot m)$ — unacceptable for large value ranges.

### 2. Optimized core idea (inverting the perspective)

Incrementing $n-1$ elements by 1 is **relatively identical** to decrementing **one** element by 1: relative distances when incrementing $n-1$ elements are no different from decrementing the single remaining element.

Goal: bring all elements down to the **minimum** $\min$. The required moves are:

$$\text{moves} = \sum_{i} (\text{nums}[i] - \min) = \sum \text{nums} - n \cdot \min$$

The closed formula ([one-pass optimization](../glossary/algebraic-one-pass.md)) answers in $\mathcal{O}(n)$ time and $\mathcal{O}(1)$ space.

---

## Implementation (Python 3)

```python
from typing import List


class Solution:
    def minMoves(self, nums: List[int]) -> int:
        """Counts the minimal moves until all elements are equal.

        Args:
            nums: Input array

        Returns:
            Minimal number of moves
        """
        # Generator expressions: O(n) time, O(1) extra space,
        # running at C speed inside the built-in functions.
        return sum(nums) - len(nums) * min(nums)
```

---

## Complexity Analysis

| Dimension                              | Complexity       | Rationale                                                                                           |
| :------------------------------------- | :--------------- | :-------------------------------------------------------------------------------------------------- |
| **[Time](../glossary/o-notation.md)**  | $\mathcal{O}(n)$ | `sum()` and `min()` traverse the list once, in C.                                                   |
| **[Space](../glossary/o-notation.md)** | $\mathcal{O}(1)$ | Generator expressions build no intermediate list ([details](../glossary/generator-expressions.md)). |

---

## Edge Cases & Pitfalls

- [x] **All elements already equal:** $\sum - n \cdot \min = 0$ — correct.
- [x] **Negative numbers:** The formula works unchanged, as it only operates on differences.
- [x] **Related task:** For increment-only moves on **all** $n$ elements see [LeetCode 3736](leetcode-3736.md) — there the maximum instead of the minimum is the target.
