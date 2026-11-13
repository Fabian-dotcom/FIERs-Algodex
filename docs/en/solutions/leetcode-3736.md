---
tags:
  - LeetCode
  - Array
  - Math
  - Greedy
  - Easy
---

# LeetCode 3736: Minimum Moves to Equal Array Elements III

- **Platform:** [LeetCode #3736](https://leetcode.com/problems/minimum-moves-to-equal-array-elements-iii/)
- **Difficulty:** Easy
- **Categories:** Array, Math, Greedy
- **Related Concepts:** [Algebraic One-Pass Optimization](../glossary/algebraic-one-pass.md) | [Memory-Efficient Generators](../glossary/generator-expressions.md) | [LeetCode 453](leetcode-453.md)

---

## Problem Statement

You are given an array `nums` of length $n$. In one move, **one** element may be **incremented** by $1$. Return the minimum number of moves until all elements are equal.

### Example

```text
Input:  nums = [2, 1, 3]
Output: 3
Explanation: [2,1,3] → [2,2,3] → [2,3,3] → [3,3,3].
```

---

## Intuition & Solution Approach

### Optimized core idea (increment-only moves → target is the maximum)

Since elements may only be **incremented**, every value must be raised to the **maximum** $\max$. The total move count is therefore the sum of all distances to the maximum:

$$\text{moves} = \sum_{i} (\max - \text{nums}[i]) = n \cdot \max - \sum \text{nums}$$

This is the [algebraic one-pass formula](../glossary/algebraic-one-pass.md) with the sign inverted compared to [LeetCode 453](leetcode-453.md) — there the target is the minimum because $n-1$ elements grow simultaneously.

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
        # Total difference of all elements to the largest element.
        # max() and sum() run at C speed as built-ins.
        max_val = max(nums)
        return len(nums) * max_val - sum(nums)
```

---

## Complexity Analysis

| Dimension                              | Complexity       | Rationale                                                   |
| :------------------------------------- | :--------------- | :---------------------------------------------------------- |
| **[Time](../glossary/o-notation.md)**  | $\mathcal{O}(n)$ | `max()` and `sum()` traverse the list once, linearly, in C. |
| **[Space](../glossary/o-notation.md)** | $\mathcal{O}(1)$ | No additional growing memory — only scalars.                |

---

## Edge Cases & Pitfalls

- [x] **All elements already equal:** $n \cdot \max - \sum = 0$ — correct.
- [x] **Negative numbers:** The formula stays valid unchanged, as it only uses differences.
- [x] **Contrast with LeetCode 453:** One element grows per move → target is `max`. $n-1$ elements grow per move → target is `min`. The perspective inversion is the key to both closed formulas.
