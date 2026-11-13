---
tags:
  - LeetCode
  - Array
  - String
  - Greedy
  - Sorting
  - Math
  - Medium
---

# LeetCode Weekly 526 Q1: Minimum Value of Merged Integers

- **Platform:** Weekly Contest 526, Q1
- **Difficulty:** Medium
- **Categories:** Array, String, Greedy, Sorting, Math
- **Related Concepts:** [String Allocation Overhead](../glossary/python-performance-optimization.md)

---

## Problem Statement

You are given an integer array `nums` of even length $n$. Merge the elements **pairwise in fixed order**: `nums[0]` with `nums[1]`, `nums[2]` with `nums[3]`, and so on. Merging two integers concatenates all decimal digits of the first followed by those of the second.

Return the **minimum value** among all resulting merged integers.

### Example

```text
Input:  nums = [23, 55, 42, 21]
Output: 2142
Explanation: The pairs are "2355" and "4221". The minimum is 2142 from "42"+"21".
```

---

## Intuition & Solution Approach

### Optimized core idea (lexicographic trick)

Concatenated numbers are best compared as **strings** — with one decisive detail: `(length, string)` tuples are the right comparison key, because `"9" > "10"` lexicographically even though $9 > 10$ numerically. Only the **length as the primary key** (a shorter number is always smaller, no leading-zero case since values are $\ge 1$), followed by the string comparison, reproduces the numeric order correctly.

1. Initialize `best` with the first pair.
2. Compare every further pair with `(len, string)` and take over if smaller.
3. Return `int(best)` at the end.

This runs in $\mathcal{O}(n)$ pair comparisons and allocates only **one** intermediate string per step.

---

## Implementation (Python 3)

```python
from typing import List


class Solution:
    def minMerged(self, nums: List[int]) -> int:
        """Finds the minimum value of all fixed-pair merged integers.

        Args:
            nums: Array of even length

        Returns:
            Minimum merged value
        """
        best = str(nums[0]) + str(nums[1])

        for i in range(2, len(nums), 2):
            merged = str(nums[i]) + str(nums[i + 1])
            # (length, string) maps the numeric order correctly
            if (len(merged), merged) < (len(best), best):
                best = merged

        return int(best)
```

---

## Complexity Analysis

| Dimension                              | Complexity               | Rationale                                            |
| :------------------------------------- | :----------------------- | :--------------------------------------------------- |
| **[Time](../glossary/o-notation.md)**  | $\mathcal{O}(n \cdot d)$ | $n/2$ pairs; each comparison costs up to $d$ digits. |
| **[Space](../glossary/o-notation.md)** | $\mathcal{O}(d)$         | Only `best` and the current `merged` are allocated.  |

---

## Edge Cases & Pitfalls

- [x] **Pure string comparisons are wrong:** `"10" < "9"` lexicographically — the length must be the primary key.
- [x] **Fixed pairing:** The pairs are fixed by the problem statement; only the minimum value is sought.
- [x] **Concatenation, not addition:** Do not confuse `str(a) + str(b)` with `a + b`.
