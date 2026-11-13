---
tags:
  - Data Structure
  - Heap
  - Priority Queue
  - Median
  - Lazy Deletion
  - Sliding Window
---

# Two-Heap with Lazy Deletion & Median Cost (L1 Norm)

The **two-heap pattern** keeps the lower and upper half of a sliding window in two balanced heaps and maintains the median as well as the sum of absolute deviations ($L_1$ norm) in amortized $\mathcal{O}(\log x)$ per step.

---

## When to use it?

- The **median** of a sliding window of size $x$ must stay up to date after every step.
- Additionally, the **sum of absolute deviations** from the median is required:
  $$\sum_{i} |a_i - \text{median}|$$
  (the classic _minimum cost to equalize_ criterion, e.g. [LeetCode 3841](../solutions/leetcode-3841.md)).
- Naively re-sorting each window would cost $\mathcal{O}(n \cdot x \log x)$ — the two-heap approach achieves $\mathcal{O}(n \log x)$.

---

## Core mechanics

### Two balanced heaps

| Heap    | Direction               | Contents   | Invariant                                       |
| :------ | :---------------------- | :--------- | :---------------------------------------------- |
| `small` | Max-heap (via negation) | lower half | $\text{len}(small) = \text{len}(large)$ or $+1$ |
| `large` | Min-heap                | upper half | every element $\ge$ every element in `small`    |

- **Even window size:** median $= \frac{small[0] + large[0]}{2}$
- **Odd window size:** median $= small[0]$ (the lower half holds the extra element)

### Lazy Deletion

Elements leaving the window are **not** expensively searched inside the heap (an $\mathcal{O}(n)$ search), but merely marked in a frequency table `invalid`:

```python
invalid[departing_element] += 1   # mark in O(1)
```

Only when such an element actually **reaches the top** of a heap is it physically cleaned up:

```python
while invalid[small[0]]:
    invalid[small[0]] -= 1
    heapq.heappop(small)
```

This avoids the linear search and amortizes the cleanup cost over all future pops.

### Median cost in $\mathcal{O}(1)$ per query

Both heaps carry running **sums** (`small_sum`, `large_sum`), giving the closed-form cost:

```python
cost = median * len(small) - small_sum + large_sum - median * len(large)
```

So the $L_1$-cost query is constant; only window maintenance costs $\mathcal{O}(\log x)$.

---

## Python skeleton

```python
import heapq
from collections import defaultdict

small, large = [], []          # max-heap (negated), min-heap
small_sum = large_sum = 0
invalid = defaultdict(int)
small_size = large_size = 0    # effective (non-lazy) sizes

def prune(heap: list, is_small: bool) -> None:
    """Physically remove marked elements at the top."""
    sign = -1 if is_small else 1
    while heap and invalid[sign * heap[0]]:
        invalid[sign * heap[0]] -= 1
        heapq.heappop(heap)

def rebalance() -> None:
    """Invariant len(small) == len(large) or len(small) == len(large)+1."""
    global small_size, large_size
    prune(small, True); prune(large, False)
    if small_size > large_size + 1:
        val = -heapq.heappop(small); small_sum -= val; small_size -= 1
        heapq.heappush(large, val); large_sum += val; large_size += 1
    elif small_size < large_size:
        val = heapq.heappop(large); large_sum -= val; large_size -= 1
        heapq.heappush(small, -val); small_sum += val; small_size += 1
```

---

## Complexity

| Operation                 | Complexity                 | Rationale                                      |
| :------------------------ | :------------------------- | :--------------------------------------------- |
| **Add element**           | $\mathcal{O}(\log x)$      | Push + rebalance.                              |
| **Remove element (lazy)** | $\mathcal{O}(1)$ amortized | Just a mark; cleanup spreads over future pops. |
| **Query median**          | $\mathcal{O}(1)$           | Top of the weighted heap.                      |
| **Query $L_1$ cost**      | $\mathcal{O}(1)$           | Closed formula from the carried sums.          |
| **Space**                 | $\mathcal{O}(x)$           | Two heaps + frequency table.                   |
