---
tags:
  - Meta
  - Changelog
  - Updates
---

# Changelog & What's New?

Chronological log of all new algorithms, data structures, LeetCode solutions, security write-ups, and architectural improvements in Algodex.

---

## November 14, 2026

### New Section: Languages & Migration (Python → Rust)
- **New glossary section [Languages & Migration](glossary/languages-rust.md):**  
  Comprehensive Python ↔ Rust translation table (collections, iterators, error handling), the most common beginner pitfalls (ownership, `Option`, integer types) and a stepped Rust learning roadmap.
- **New strategy:** From now on, every new glossary chapter documents the reference in **both** languages – Python first, plus a Rust variant with language-specific "Rust Notes".
- **Added retroactively:** [Sliding Window](glossary/sliding-window.md) extended with its Rust reference implementation.

### New Glossary Entries (Core Algodex)
- **[Monotonic Stack with Cost Accumulation (Backward Sliding Window)](glossary/monotonic-stack-cost-accumulation.md):**
  Backward sweep for subarray repair costs (e.g. non-decreasing): a monotonic stack manages local peaks/valleys, costs are updated incrementally, and a second pointer `j` shrinks the window against budget `k`. $
\mathcal{O}(n)$ time, $
\mathcal{O}(n)$ space – documented in Python **and** Rust.
- **[Disjoint Set Union (DSU / Union-Find)](glossary/dsu-union-find.md):**
  Dynamic connectivity with `find` & `union`, path compression and union by size in almost $
\mathcal{O}(1)$ ($
\alpha(n)$) per operation – Kruskal, island clusters, online connectivity queries. Also documented twice (Python & Rust, including the `&mut self` lesson).
- **Keyword reference, changelog and both MkDocs navigations (`mkdocs.yml`, `mkdocs.en.yml`) extended.**

---

## November 7, 2026

### Advanced Heap & Simulation Patterns (Core Algodex)
- **[Two-Heap with Lazy Deletion & Median Cost (L1 Norm)](glossary/two-heap-lazy-deletion.md):**
  Balanced max-/min-heaps for sliding-window medians; departed elements are marked in a frequency table instead of being searched, and the $L_1$ deviation sum is answered in $\mathcal{O}(1)$ from carried half-sums.
- **[Sorted Queries with Two-Pointer Window (Event Tracking)](glossary/sorted-queries-two-pointer.md):**
  Queries sorted as `(value, original_index)` tuples and co-swept monotonically with the time-sorted log — no redundant searches, optimal $\mathcal{O}(n \log n + k \log k)$.
- **[Event-Driven Simulation with Two Priority Queues (Time Jumps)](glossary/event-driven-simulation.md):**
  Free heap (weight, then index) and busy heap (completion time) model continuous scheduling; `current_time = busy_servers[0][0]` jumps straight to the next event instead of ticking per second.
- **Keyword Reference, changelog and both MkDocs navigations (`mkdocs.yml`, `mkdocs.en.yml`) extended accordingly.**

### New documented LeetCode solutions
- **[LC 1882 – Process Tasks Using Servers](solutions/leetcode-1882.md):** Two heaps + time jump — the reference implementation of the [event-driven simulation pattern](glossary/event-driven-simulation.md).
- **[LC 2747 – Count Zero Request Servers](solutions/leetcode-2747.md):** Sorted queries with two pointers + frequency table ([pattern reference](glossary/sorted-queries-two-pointer.md)).
- **[LC 3505 – Minimum Operations (K Subarrays Equal)](solutions/leetcode-3505.md):** Two-heap with lazy deletion for window medians + memory-optimized bottom-up DP ([pattern reference](glossary/two-heap-lazy-deletion.md)).
- **[LC 453](solutions/leetcode-453.md) & [LC 3736](solutions/leetcode-3736.md) – Minimum Moves I/III:** Closed formulas $\sum - n \cdot \min$ and $n \cdot \max - \sum$ as a perspective inversion.
- **[Weekly Contest 526 Q1–Q4](solutions/leetcode-w526-q1.md):** (length, string) ordering, smallest-prime-factor chain, inversions + mandatory boundaries via Fenwick, parity decomposition in iterative tree DP.
- **New glossary chapter [Python Performance Optimizations](glossary/python-performance-optimization.md):** zero-copy indexing vs. slicing, string allocation overhead, generator expressions and built-in C speed.
- **Cross-links:** LC 1851 ↔ 2747 and LC 3841 ↔ 1882 are now cross-referenced.

---

## November 4, 2026

### Multi-Language Architecture (i18n)
- **Official Material Multi-Site Setup (German & English):**  
  Full bilingual deployment across `/de/` and `/en/`.
- **Completely Isolated Search Indices:**  
  Each language builds into its own site bundle with its own dedicated `search_index.json`. Searching in English returns zero duplicate German hits, and vice versa.
- **Native Header Language Selector:**  
  Toggle seamlessly between German and English via the top-right header language dropdown powered by `extra.alternate`.
- **Smart Root Redirect:**  
  Visitors to the root domain are automatically forwarded to `/de/` or `/en/` according to browser language preferences.

---

## October 31, 2026

### Platform Architecture & UX Relaunch
- **Interactive Control Center on Home:** Guided routes for interviews, graph theory, web security, and discrete math.
- **FIER's Red Algodex Decoupling:** Standalone offensive security and bug bounty hub with specialized dark-red branding.
- **Categorized Sidebar & Tabs:** Grouped glossary entries into collapsible sections.
- **SVG GitHub Header Banner:** Responsive vector banner for the repository homepage.

---

## October 30, 2026

### Core Algorithms & Concepts
- State-Space Dijkstra, CSR Format, PageRank, Graph Neural Networks, SpMV with SciPy, Memory Management, BFS/DFS, Topological Sort, Big-O Complexity Graph.
- 18 comprehensively documented LeetCode solutions (LC 1, 2, 3, 4, 9, 12, 13, 1254, 1360, 1851, 2409, 2791, 3619, 3644, 3841, 3942, 3963, 3970).
