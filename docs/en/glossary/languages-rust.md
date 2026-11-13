---
tags:
  - Rust
  - Python
  - Languages
  - Learning
---

# Languages & Migration (Python → Rust)

This section is the home of all **language-specific** documentation. The Algodex historically builds on Python (`python`/`python3` code blocks); here we learn to read and write the same algorithms in **Rust**, and to weigh the language characteristics against each other.

---

## Why Rust for Algorithms?

| Aspect               | Python                                   | Rust                                                                                                      |
| :------------------- | :--------------------------------------- | :-------------------------------------------------------------------------------------------------------- |
| **Type system**      | Dynamic, optional type hints             | Static, checked at compile time                                                                           |
| **Integer overflow** | Automatic unbounded big ints             | Fixed widths (`i32`, `i64`, `u64`, …) – choose sums deliberately                                          |
| **Memory model**     | Garbage collector, heap objects          | Ownership & borrow checker, deterministic at compile time (see [Memory Management](memory-management.md)) |
| **Speed**            | Interpreter, C built-ins as accelerators | Native machine code, competing with C/C++                                                                 |
| **Collections**      | `list`, `dict`, `collections.deque`      | `Vec`, `HashMap`, `VecDeque`                                                                              |
| **Getting started**  | One-line script                          | `cargo new`, type annotations, borrowing rules                                                            |

---

## Python ↔ Rust Translation Table

| Python                                           | Rust                                                                | Note                                            |
| :----------------------------------------------- | :------------------------------------------------------------------ | :---------------------------------------------- |
| `arr = [0] * n`                                  | `let arr = vec![0; n];`                                             | Preallocation, no re-alloc                      |
| `for i, x in enumerate(arr):`                    | `for (i, &x) in arr.iter().enumerate()`                             | `&x` dereferences the reference                 |
| `for i in reversed(range(n))`                    | `for i in (0..n).rev()`                                             | Ranges instead of index functions               |
| `list.append(x)` / `list.pop()`                  | `vec.push(x)` / `vec.pop()`                                         |                                                 |
| `collections.deque` (`append`, `pop`, `popleft`) | `std::collections::VecDeque` (`push_back`, `pop_back`, `pop_front`) | $\mathcal{O}(1)$ on both ends                   |
| `heapq` (`heappush`, `heappop`)                  | `std::collections::BinaryHeap` (max-heap; min via `Reverse`)        | Rust std has no min-heap directly               |
| `d = {}` / `d[k] = v`                            | `let mut d = HashMap::new();` / `d.insert(k, v);`                   | Access via `d.get(&k)` yields `Option<&V>`      |
| `sorted(arr)`                                    | `arr.sort()` (in place) or `arr.to_vec().sort()`                    | `sort_unstable()` is faster but not stable      |
| `arr[-1]`                                        | `*arr.last().unwrap()` or `arr[arr.len() - 1]`                      | Negative indices do not exist                   |
| `a, b = b, a + b`                                | `(a, b) = (b, a + b);`                                              | Tuple swap since Rust 1.59                      |
| `max(x, default=0)`                              | `x.max(0)`                                                          | Methods instead of built-ins                    |
| `float("inf")`                                   | `i64::MAX` / `f64::INFINITY`                                        | Type dependent                                  |
| `if x not in seen:`                              | `if !seen.contains(&x)` (set)                                       | `&` required for borrowed types                 |
| `f-strings f"{x}"`                               | `format!("{x}")`                                                    | Same `{}` syntax                                |
| `class Node:`                                    | `struct Node { ... }`                                               | Structs instead of classes; behavior via `impl` |
| `None`                                           | `Option<T>` (`None` / `Some(t)`)                                    | No `null` – the compiler forces handling        |
| Exceptions (`raise`)                             | `Result<T, E>` (`Err` / `?` operator)                               | Errors are values, not stack unwinds            |

---

## Rust Concepts You Keep Stumbling Over at First

1. **Ownership & Borrowing:** Every value has exactly one owner. `&x` reads (any number), `&mut x` writes (only one at a time). The DSU implementation ([Union-Find](dsu-union-find.md)) shows why `find` needs `&mut self`: path compression writes.
2. **`Option` instead of `None` checks:** `stack.back().copied().unwrap_or(j)` is the Rust idiom for `stack[-1] if stack else j` (see [Monotonic Stack](monotonic-stack-cost-accumulation.md)).
3. **Choose integer types deliberately:** `usize` for indices/lengths, `i64` for sums. For $n \cdot \max(\text{val})$ beyond $10^{18}$ → `i128`.
4. **`while let Some(x) = ...`:** Rust's idiomatic pattern for „as long as there is something" – corresponds to Python's `while stack:`.
5. **Iterators instead of loop indices:** `(0..n).map(...).sum()` often compiles to the same machine loop as the handwritten `for` version – iterators are **not** slower.

---

## Rust Learning Roadmap (Recommended Path)

1. **Syntax & control flow:** Variables (`let mut`), functions, `match` instead of `switch`.
2. **Collections:** `Vec`, `VecDeque`, `HashMap`, `String` vs `&str`.
3. **Ownership basics:** Move semantics, references, lifetime intuition (not yet explicit lifetimes).
4. **Port the first algorithms:** The simple glossary patterns first (e.g. [Sliding Window](sliding-window.md)), then [DSU](dsu-union-find.md) with `&mut self`.
5. **Traits & generics:** `impl`, `derive(Debug)`, custom traits for heap comparisons (`Ord`).
6. **Result & error handling:** Keep LeetCode-style signatures `fn f(...) -> Result<i64, String>` in mind.

---

## Strategy in the Algodex

From now on, every **new** glossary chapter documents the reference in **both** languages: Python first (history, fast iteration) plus the Rust variant with language-specific pitfalls in its own _„Rust Notes"_ sub-section. Existing chapters are extended step by step – starting with [Sliding Window](sliding-window.md), [Monotonic Stack with Cost Accumulation](monotonic-stack-cost-accumulation.md) and [DSU / Union-Find](dsu-union-find.md).
