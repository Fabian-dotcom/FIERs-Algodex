---
tags:
  - Overview
  - Home
  - Core
---

# FIER's Algodex

The interactive developer wiki and reference guide for **algorithms**, **data structures**, **LeetCode solutions in Python 3**, and **offensive web security** – rigorous, concise, and clearly explained.

[Core Algodex (Python & LeetCode)](roadmaps/graphs.md){ .md-button .md-button--primary }
[Red Algodex (Security Hub)](red-algodex/index.md){ .md-button style="background-color: #b71c1c; color: white; border-color: #b71c1c;" }
[Keyword Reference (A-Z)](references.md){ .md-button }

---

## Structured Learning Paths

Choose a guided route to navigate through the topics chronologically:

### Coding Interview Preparation
The concise roadmap covering essential algorithm patterns for technical interviews.

1. [Landau Symbols & Big-O Notation](glossary/o-notation.md)
2. [Hash Map & Two Sum Complement](glossary/hash-map.md)
3. [Sliding Window Pattern](glossary/sliding-window.md)
4. [Binary Search & Partitioning](glossary/binary-search.md)

[Go to Arrays & Strings Path](roadmaps/arrays-strings.md){ .md-button }

---

### Graph Theory & Trees from Zero to Hero
From memory representations to advanced tree and pathfinding techniques.

1. [Adjacency List](glossary/adjazenzliste.md) & [CSR Format](glossary/csr-format.md)
2. [Graph Traversal (BFS & DFS)](glossary/traversierung-bfs-dfs.md)
3. [State-Space Dijkstra](glossary/state-space-dijkstra.md)
4. [Binary Lifting & LCA](glossary/advanced-tree-techniques.md)

[Go to Graphs & Trees Path](roadmaps/graphs.md){ .md-button }

---

### Web Security & Bug Bounty Basics
Introduction to offensive security following PortSwigger and OWASP standards.

1. [Web Fundamentals (HTTP, SOP, CORS, CSP)](red-algodex/vulnerabilities/http-sop-cors-csp.md)
2. [Burp Suite Fundamentals & Proxy Mastery](red-algodex/tools/burp-suite-basics.md)
3. [Cross-Site Scripting (XSS)](red-algodex/vulnerabilities/xss.md)
4. [SQL Injection (SQLi)](red-algodex/vulnerabilities/sqli.md)

[Go to Red Algodex Hub](red-algodex/index.md){ .md-button style="background-color: #b71c1c; color: white; border-color: #b71c1c;" }

---

### Discrete Math & Bit Manipulation
High-performance problem solving at the bit level in minimal CPU cycles.

1. [Bitwise Operations & Bitmasks](glossary/bit-manipulation.md)
2. [Palindrome Bit Trick in O(1)](glossary/bit-manipulation.md)
3. [Mathematical Number Reversal](glossary/math-number-reversal.md)
4. [Cyclic Permutations](glossary/cyclic-permutations.md)

[Go to Math & Bits Path](roadmaps/math-bit-manipulation.md){ .md-button }

---

## Quick Access

=== "Concepts & Data Structures"

    - [State-Space Dijkstra](glossary/state-space-dijkstra.md) – Shortest path with history, rules, and state-space reduction.
    - [Constraint-Driven Design](glossary/constraint-driven-design.md) – Small constraints as architectural hints for DP and bitmasks.
    - [CSR Format (Compressed Sparse Row)](glossary/csr-format.md) – Contiguous 1D arrays for cache-friendly graphs and sparse matrices.
    - [Big-O Notation & Complexity](glossary/o-notation.md) – Interactive SVG growth chart from $\mathcal{O}(1)$ to $\mathcal{O}(n!)$.
    - [Algebraic One-Pass Optimization](glossary/algebraic-one-pass.md) – Single-pass sum reduction $\mathcal{O}(n)$ instead of nested scans.
    - [Memory-Efficient Generators](glossary/generator-expressions.md) – True $\mathcal{O}(1)$ extra memory via lazy evaluation.
    - [Advanced Tree Techniques](glossary/advanced-tree-techniques.md) – Lowest Common Ancestor (LCA), Binary Lifting, Euler Tour, Fenwick Tree.
    - [Sliding Window](glossary/sliding-window.md) – Dynamic two-pointer intervals and ASCII array tuning.
    - [Memory Management & GC](glossary/memory-management.md) – Pointer overhead, cache lines, and language paradigms (Python, Java, Rust, C++).

=== "Challenging Solutions (Hard)"

    - [LeetCode 3970: Shortest Path With At Most K Consecutive Characters](solutions/leetcode-3970.md) – State-space Dijkstra with min-heap $\mathcal{O}((E \cdot k) \log(V \cdot k))$.
    - [LeetCode 3841: Palindromic Path Queries in a Tree](solutions/leetcode-3841.md) – Dynamic tree updates via Euler Tour, Binary Lifting, and Fenwick Tree.
    - [LeetCode 2791: Count Paths That Can Form a Palindrome in a Tree](solutions/leetcode-2791.md) – Prefix-XOR, 26-bit masks, and DFS.
    - [LeetCode 1851: Minimum Interval to Include Each Query](solutions/leetcode-1851.md) – Sweep-line with min-heap and lazy invalidation $\mathcal{O}((n + k) \log(n + k))$.
    - [LeetCode 4: Median of Two Sorted Arrays](solutions/leetcode-4.md) – Binary search on two-array partitioning in $\mathcal{O}(\log(\min(m, n)))$.

=== "Offensive Security (Red Algodex)"

    - [Red Algodex Hub](red-algodex/index.md) – Dedicated offensive security and bug bounty section.
    - [Burp Suite Basics](red-algodex/tools/burp-suite-basics.md) – Proxy, Repeater, Intruder, Collaborator, and Autorize extension.
    - [Cross-Site Scripting (XSS)](red-algodex/vulnerabilities/xss.md) – Reflected, Stored, and DOM-based XSS, Sources/Sinks, CSP.
    - [SQL Injection (SQLi)](red-algodex/vulnerabilities/sqli.md) – Union-Based, Error-Based, Blind SQLi, and Prepared Statements.
    - [Server-Side Request Forgery (SSRF)](red-algodex/vulnerabilities/ssrf.md) – Cloud metadata (AWS IMDS), filter bypasses, OAST.
    - [Broken Access Control & IDOR](red-algodex/vulnerabilities/access-control-idor.md) – Object-level authorization flaws and privilege escalation.

=== "Reference & Community"

    - [Keyword Reference Index](references.md) – Alphabetical index of all documented concepts.
    - [Changelog (What's New)](changelog.md) – Chronological release history of algorithms and features.
    - [GitHub Repository](https://github.com/Fabian-dotcom/fiers-algodex) – Source code, issues, and contribution guidelines.
    - [GitHub Sponsor / Buy me a coffee](https://github.com/sponsors/Fabian-dotcom) – Support continuous maintenance.

---

## Documentation Standards

Every article in Algodex adheres to a standardized structure:

1. **Intuition & Core Idea:** High-level conceptual explanation before writing code.
2. **Mermaid.js Visualizations:** Graphical trees, state transitions, and memory layouts rendered in-browser.
3. **Python 3 Implementation:** Strictly typed code using `typing` (`List`, `Tuple`, `Dict`, `Optional`) with detailed comments.
4. **Complexity Analysis:** Rigorous breakdown of time ($\mathcal{O}(T)$) and space ($\mathcal{O}(S)$) requirements.
5. **Edge Cases & Gotchas:** Key pitfalls (empty inputs, duplicates, recursion limits, integer overflows).

---

## Navigation & Search

Use the navigation tabs above to switch between **Core Algodex** and **Red Algodex**, the sidebar on the left, or press <kbd>s</kbd> or <kbd>/</kbd> for instant full-text search.
