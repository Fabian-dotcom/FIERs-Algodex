---
tags:
  - Python
  - Performance
  - Optimization
  - Memory
  - Benchmark
---

# Python Performance Optimizations: Zero-Copy, String Overhead & C Speed

Micro-optimizations that make the difference between TLE and Accepted in performance-critical tasks (time limits on large inputs) — without changing the algorithm.

---

## 1. Zero-Copy Indexing vs. Slicing

| Variant                                     | Memory behavior                  | Complexity                |
| :------------------------------------------ | :------------------------------- | :------------------------ |
| **Slicing** `arr[::2]`                      | Creates a **new list** in memory | $\mathcal{O}(n)$ overhead |
| **Index iterators** `range(0, len(arr), 2)` | Access indices directly, no copy | $\mathcal{O}(1)$ space    |

```python
# copy overhead: builds a second list
halves = arr[::2]

# zero-copy: iterates over indices only
for i in range(0, len(arr), 2):
    x = arr[i]
```

The slice allocator can allocate gigabyte-scale copies repeatedly on large arrays or inside tight loops; index iterators stay completely copy-free ([related: generator expressions](generator-expressions.md)).

---

## 2. Generator Expressions in Aggregate Functions

Passing a generator (**without square brackets** `[...]`) into `min()`, `max()`, `sum()` computes values _on-the-fly_ (lazy evaluation) — the list is **never built as a whole** in an intermediate buffer:

```python
total = sum(x * x for x in nums)      # O(1) extra space
total = sum([x * x for x in nums])    # O(n) extra space (a real list!)
```

More details and pitfalls: [Memory-Efficient Generators](generator-expressions.md).

---

## 3. String Allocation Overhead

String operations (`str()`, concatenation, `int()`) are **noticeably slower** than purely arithmetic operations on large data, because they require heap memory allocations:

- Every concatenation `a + b` allocates a new string object.
- `int(s)` / `str(n)` cost parsing/formatting per digit.
- **Rule:** digit logic (modulo, division, `bit_count()`) beats string detours — see [Mathematical Number Reversal](math-number-reversal.md).

A showcase: when comparing merged integers ([Weekly 526 Q1](../solutions/leetcode-w526-q1.md)) string concatenation is unavoidable — everywhere else, the arithmetic variant is preferable.

---

## 4. Implicit Loop Optimization (Built-in C Speed)

Python built-in functions (`sum()`, `min()`, `max()`, `sorted()`) combined with generator expressions execute in **C, extremely close to hardware speed**, even when conceptually every element is visited once ($\mathcal{O}(n)$):

```python
# C-level loop: faster than an equivalent Python for-loop
best = max((f(x) for x in nums), default=0)
```

Additionally, for heap-heavy code, **local binding** of hot-path functions pays off ([LeetCode 1851](../solutions/leetcode-1851.md)):

```python
heappush = heapq.heappush
heappop = heapq.heappop
```

This eliminates the attribute lookup (`heapq.`) on every call inside tight sweeps.

---

## When to use it?

- **TLE despite a correct algorithm:** check these four levers first, then change the data structure.
- **Memory limits:** slicing → index iterator, list comprehension → generator.
- **Do not over-optimize:** readability beats micro-gains as long as no limit is affected.
