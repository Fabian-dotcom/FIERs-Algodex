---
tags:
  - Meta
  - Changelog
  - Updates
---

# Changelog & Was ist neu?

Hier werden alle neuen Algorithmen, Datenstrukturen, LeetCode-Lösungen und strukturellen Erweiterungen des Algodex chronologisch dokumentiert.

---

## 30. Oktober 2026

### Neue Algorithmen & Glossar-Konzepte
- **[Zustandsbasierter Dijkstra (State-Space Dijkstra)](glossary/state-space-dijkstra.md):**  
  Erweiterung des Dijkstra-Algorithmus um Pfad-Historien und Zustandsraum-Reduktion `(u, last_char, count)`.
- **[CSR-Format (Compressed Sparse Row)](glossary/csr-format.md):**  
  Flache 1D-Arrays (`row_ptr`, `targets`, `weights`) zur Vermeidung von Pointer-Overhead und Maximierung der Cache-Lokalität.
- **[PageRank-Algorithmus](glossary/pagerank.md):**  
  Random-Surfer-Modell, Dämpfungsfaktor $d$ und Power Iteration im CSR-Format.
- **[Graph Neural Networks (GNN)](glossary/gnn.md):**  
  Message Passing, Node Embeddings und GPU-beschleunigte SpMM.
- **[SciPy & Matrix-Vektor-Multiplikation (SpMV)](glossary/scipy-matrix-vector.md):**  
  Dünnbesetzte Multiplikationen $\mathbf{y} = \mathbf{A}\mathbf{x}$ in $\mathcal{O}(E)$ mit NumPy/SciPy.
- **[Speicherverwaltung & Garbage Collection](glossary/memory-management.md):**  
  64-Byte Cache-Lines, Pointer-Overhead und Sprachvergleich (Python, Java, Rust, C++).
- **[Graph-Traversierung (BFS & DFS)](glossary/traversierung-bfs-dfs.md):**  
  Breiten- und Tiefensuche, schichtweise Erkundung und iterativer Stack.
- **[Topologische Sortierung](glossary/topologische-sortierung.md):**  
  Kahn-Algorithmus mit In-Degree Queue und Zykluserkennung in DAGs.
- **[Landau-Symbole & Big-O Notation](glossary/o-notation.md):**  
  Interaktives SVG-Wachstumsdiagramm und Sprungtabelle von $\mathcal{O}(1)$ bis $\mathcal{O}(n!)$.

### Web Security & Bug Bounty (Red Algodex)
- **[Lernpfad: Web Security & Bug Bounty Hunting](red-algodex/roadmaps/web-security.md):** Chronologischer Lernweg von PortSwigger-Labs über OWASP Top 10 bis hin zu Reconnaissance.
- **[Burp Suite Grundlagen](red-algodex/tools/burp-suite-basics.md):** Proxy, Repeater, Intruder, Decoder, Collaborator und BApp Extensions (Autorize, Turbo Intruder).
- **[Cross-Site Scripting (XSS)](red-algodex/vulnerabilities/xss.md):** Reflected, Stored und DOM-based XSS, Sources/Sinks, WAF-Evasion und CSP.
- **[SQL Injection (SQLi)](red-algodex/vulnerabilities/sqli.md):** Union-Based, Error-Based, Blind SQLi (Boolean/Time) und Prepared Statements.
- **[Server-Side Request Forgery (SSRF)](red-algodex/vulnerabilities/ssrf.md):** Cloud-Metadaten (AWS IMDS), IP-Filter-Bypasses, DNS Rebinding und Blind SSRF.
- **[Broken Access Control & IDOR](red-algodex/vulnerabilities/access-control-idor.md):** Horizontale/vertikale Rechteausweitung und automatisierte IDOR-Erkennung mit Autorize.

### Neue Lernpfade
- **[Lernpfad: Arrays, Strings & Sequenz-Muster](roadmaps/arrays-strings.md):** Two Pointers, Sliding Window, Sweep-Line und Binäre Suche.
- **[Lernpfad: Dynamische Programmierung (DP)](roadmaps/dynamic-programming.md):** Memoization, Tabulation, Knapsack und Zustandsräume.
- **[Lernpfad: Mathematik & Bit-Manipulation](roadmaps/math-bit-manipulation.md):** Bitmasken, Akkumulierendes Bit-AND und Prefix-XOR.

### Neue LeetCode-Lösungen
- **[LeetCode 3970: Shortest Path With At Most K Consecutive Identical Characters](solutions/leetcode-3970.md)** (Hard)
- **[LeetCode 3963: Create Grid With Exactly One Path](solutions/leetcode-3963.md)** (Medium)
- **[LeetCode 3942: Minimum Operations to Sort a Permutation](solutions/leetcode-3942.md)** (Medium)
- **[LeetCode 3841: Palindromic Path Queries in a Tree](solutions/leetcode-3841.md)** (Hard)
- **[LeetCode 3644: Maximum K to Sort a Permutation](solutions/leetcode-3644.md)** (Medium)
- **[LeetCode 3619: Count Islands With Total Value Divisible by K](solutions/leetcode-3619.md)** (Medium)
- **[LeetCode 2409: Count Days Spent Together](solutions/leetcode-2409.md)** (Easy)
- **[LeetCode 1851: Minimum Interval to Include Each Query](solutions/leetcode-1851.md)** (Hard)
- **[LeetCode 1360: Number of Days Between Two Dates](solutions/leetcode-1360.md)** (Easy)
- **[LeetCode 1254: Number of Closed Islands](solutions/leetcode-1254.md)** (Medium)
- **[LeetCode 13: Roman to Integer](solutions/leetcode-13.md)** (Easy)
- **[LeetCode 12: Integer to Roman](solutions/leetcode-12.md)** (Medium)
- **[LeetCode 9: Palindrome Number](solutions/leetcode-9.md)** (Easy)
- **[LeetCode 4: Median of Two Sorted Arrays](solutions/leetcode-4.md)** (Hard)
- **[LeetCode 3: Longest Substring Without Repeating Characters](solutions/leetcode-3.md)** (Medium)
- **[LeetCode 2: Add Two Numbers](solutions/leetcode-2.md)** (Medium)
- **[LeetCode 1: Two Sum](solutions/leetcode-1.md)** (Easy)

### System- & UI-Erweiterungen
- **Zentrale Stichwort-Referenz ([`docs/references.md`](references.md)):** Alphabetischer Index aller behandelten Themen.
- **Quick-Access Cards & Interaktive Roadmaps:** Startseite bietet direkten Absprung und Todo-Checklisten.
- **Cross-Linking:** Kontextsensitive Verlinkung aller Fachbegriffe ohne Selbstreferenzen.
