---
tags:
  - Übersicht
  - Home
---

# FIER's Algodex

> Ein persönliches, interaktives Nachschlagewerk und Lern-Wiki für **Algorithmen**, **Datenstrukturen** und **LeetCode-Lösungen in Python 3** – mathematisch fundiert, praxisnah und in eigenen Worten aufbereitet.

---

## Schnellzugriff (Quick-Access Cards)

Hier findest du direkten Zugang zu den meistgenutzten Grundlagen und anspruchsvollsten Algorithmen:

=== "Konzepte & Datenstrukturen"

    - **[Zustandsbasierter Dijkstra](glossary/state-space-dijkstra.md):** Kürzeste Pfade mit Historien, Zeichenfolgen und State-Space Reduction.
    - **[CSR-Format (Compressed Sparse Row)](glossary/csr-format.md):** Flache, cache-optimierte 1D-Arrays für Graphen und Sparse-Matrizen.
    - **[Landau-Symbole & Big-O Notation](glossary/o-notation.md):** Interaktives Wachstumsdiagramm und Komplexitätsanalyse von $\mathcal{O}(1)$ bis $\mathcal{O}(n!)$.
    - **[Fortgeschrittene Baum-Techniken](glossary/advanced-tree-techniques.md):** Lowest Common Ancestor (LCA), Binary Lifting, Euler-Tour und Fenwick-Bäume.
    - **[Schiebefenster (Sliding Window)](glossary/sliding-window.md):** Dynamische Two-Pointer-Fenster und ASCII-Array-Optimierung.
    - **[Speicher & Garbage Collection](glossary/memory-management.md):** Pointer-Overhead, Cache-Lines und Sprachvergleich (Python, Java, Rust, C++).

=== "Herausfordernde Lösungen (Hard)"

    - **[LeetCode 3970: Shortest Path With At Most K Consecutive Characters](solutions/leetcode-3970.md):** Zustandsbasierter Dijkstra mit Min-Heap und State-Space Expansion $\mathcal{O}((E \cdot k) \log(V \cdot k))$.
    - **[LeetCode 3841: Palindromic Path Queries in a Tree](solutions/leetcode-3841.md):** Dynamische Baum-Updates via Euler-Tour, Binary Lifting und Fenwick-Baum.
    - **[LeetCode 2791: Count Paths That Can Form a Palindrome in a Tree](solutions/leetcode-2791.md):** Prefix-XOR, 26-Bit-Masken und DFS auf Adjazenzlisten.
    - **[LeetCode 1851: Minimum Interval to Include Each Query](solutions/leetcode-1851.md):** Sweep-Line mit Min-Heap und Lazy Invalidation in $\mathcal{O}((n + k) \log(n + k))$.
    - **[LeetCode 4: Median of Two Sorted Arrays](solutions/leetcode-4.md):** Binäre Suche auf der Partitionierung zweier sortierter Arrays in $\mathcal{O}(\log(\min(m, n)))$.

=== "Web Security & Bug Bounty"

    - **[Burp Suite Grundlagen](glossary/burp-suite-basics.md):** Proxy, Repeater, Intruder und BApp Extensions (Autorize, Turbo Intruder).
    - **[Cross-Site Scripting (XSS)](glossary/web-sec-xss.md):** Reflected, Stored und DOM-based XSS, Sources/Sinks und CSP.
    - **[SQL Injection (SQLi)](glossary/web-sec-sqli.md):** Union-Based, Error-Based und Blind SQLi (Boolean/Time) sowie Prepared Statements.
    - **[Server-Side Request Forgery (SSRF)](glossary/web-sec-ssrf.md):** Cloud-Metadaten (AWS IMDS), Filter-Bypasses und OAST.
    - **[Broken Access Control & IDOR](glossary/web-sec-access-control-idor.md):** Horizontale/vertikale Rechteausweitung und automatisierte Bypasses mit Autorize.
    - **[Lernpfad: Web Security & Bug Bounty](roadmaps/web-security.md):** Chronologischer Schritt-für-Schritt-Guide von PortSwigger bis Recon.

=== "Referenzen & Community"

    - **[Stichwort-Referenz (Keyword Index)](references.md):** Vollständiges alphabetisches Begriffsverzeichnis aller Algorithmen.
    - **[Changelog (What's New)](changelog.md):** Chronologische Übersicht über neue Algorithmen, Lernpfade und Features.
    - **[GitHub Repository](https://github.com/Fabian-dotcom/fiers-algodex):** Sourcecode, Issues und Beitragsrichtlinien.
    - **[GitHub Sponsor / Buy me a coffee](https://github.com/sponsors/Fabian-dotcom):** Unterstütze die Weiterentwicklung dieses Wikis.

---

## Interaktive Roadmap & Lernfortschritt

Nutze diese interaktiven Checklisten, um deinen persönlichen Lernfortschritt strukturiert nachzuverfolgen:

### 1. Grundlagen & Lineare Strukturen
- [x] **[Landau-Symbole & Big-O Notation](glossary/o-notation.md):** Asymptotische Laufzeiten und Speicherkomplexität verstehen.
- [x] **[Hash Map & Hash Set](glossary/hash-map.md):** Schnelle $\mathcal{O}(1)$-Lookups und das Two-Sum-Komplement-Muster.
- [x] **[Verkettete Liste](glossary/linked-list.md):** ListNode-Architektur, Dummy-Head-Pattern und schriftliche Addition.
- [x] **[Schiebefenster (Sliding Window)](glossary/sliding-window.md):** Dynamische Fenster, Substrings ohne Duplikate und ASCII-Array-Tuning.
- [x] **[Binäre Suche](glossary/binary-search.md):** Logarithmischer Suchraum und Partitionierung zweier sortierter Arrays.
- [ ] **Two Pointers:** Kollidierende Zeiger und Intervalle (Two Sum II, 3Sum, Container With Most Water).

### 2. Graphen, Bäume & Kürzeste Pfade
- [x] **[Adjazenzliste](glossary/adjazenzliste.md) & [Adjazenzmatrix](glossary/adjazenzmatrix.md):** Wann Speicherplatz $\mathcal{O}(V + E)$ einer $\mathcal{O}(V^2)$-Matrix überlegen ist.
- [x] **[CSR-Format (Compressed Sparse Row)](glossary/csr-format.md):** Flache Arrays statt Listen-Overhead für maximale Cache-Lokalität.
- [x] **[Graph-Traversierung (BFS & DFS)](glossary/traversierung-bfs-dfs.md):** Schichtweise Breitensuche vs. Tiefensuche mit manuellem Stack.
- [x] **[Flood Fill & Gitter-Traversierung](glossary/flood-fill.md):** Randeliminierung (Boundary Invalidation) und In-Place Fluten.
- [x] **[Topologische Sortierung](glossary/topologische-sortierung.md):** Kahn-Algorithmus mit In-Degree Queue und Zykluserkennung in DAGs.
- [x] **[Zustandsbasierter Dijkstra](glossary/state-space-dijkstra.md):** Kürzeste Pfade mit Zustandsraum-Reduktion und Min-Heap.
- [x] **[Fortgeschrittene Baum-Techniken](glossary/advanced-tree-techniques.md):** Lowest Common Ancestor (LCA) via Binary Lifting, Euler-Tour und Fenwick-Baum.

### 3. Mathematik, Diskrete Strukturen & Bit-Tricks
- [x] **[Mathematische Zahlenumkehr](glossary/math-number-reversal.md):** Modulo/Divisions-Zerlegung und Palindrom-Check ohne String-Allokation.
- [x] **[Römische Zahlen & Ziffernsysteme](glossary/roman-numerals.md):** Greedy-Zerlegung und Rückwärts-Traversierung.
- [x] **[Datums- & Kalender-Arithmetik](glossary/date-arithmetic.md):** Gregorianische Schaltjahres-Formeln und Epochentage.
- [x] **[Bitweise Operationen & Bitmasken](glossary/bit-manipulation.md):** AND, OR, XOR, Shifts und akkumulierendes Bit-AND.
- [x] **[Palindrom-Bit-Trick](glossary/bit-manipulation.md):** Paritätsprüfung in $\mathcal{O}(1)$ über `mask & (mask - 1) == 0`.
- [x] **[Zyklische Permutationen](glossary/cyclic-permutations.md):** Invarianz-Prüfung und minimale Sortieroperationen (Shift & Reverse).

### 4. Dynamische Programmierung & Fortgeschrittenes
- [x] **[Zustandsbasierte DP auf Graphen](glossary/state-space-dijkstra.md):** Zustandsraum-Erweiterung und Relaxation.
- [ ] **1D- & 2D-Tabulation:** Longest Increasing Subsequence (LIS), Longest Common Subsequence (LCS).
- [ ] **Rucksack-Probleme (Knapsack):** 0/1 Knapsack, Subset Sum, Unbounded Knapsack.
- [ ] **Bitmask-DP:** Hamilton-Pfade und Traveling Salesperson Problem in $\mathcal{O}(2^n \cdot n^2)$.
- [x] **[Graph Neural Networks (GNN)](glossary/gnn.md) & [PageRank](glossary/pagerank.md):** Message Passing und Power Iteration auf relationalen Graphen.

### 5. Web Security & Bug Bounty Hunting
- [x] **[Burp Suite Mastery](glossary/burp-suite-basics.md):** Proxy, Intercept, Repeater, Intruder und BApp Extensions.
- [x] **[Client-Side Angriffe (XSS)](glossary/web-sec-xss.md):** Reflected, Stored und DOM-based XSS mit WAF-Evasion.
- [x] **[Server-Side Angriffe (SQLi & SSRF)](glossary/web-sec-sqli.md):** Union-, Error- und Blind-Injections sowie Cloud-Metadaten-Extraktion.
- [x] **[Autorisierungsfehler (IDOR & Access Control)](glossary/web-sec-access-control-idor.md):** Objekt-Level Autorisierung und horizontal/vertikal Escalation.
- [ ] **Reconnaissance & Automatisierung:** Asset Discovery, Fuzzing (`ffuf`), Endpunktextraktion und verantwortungsvolles Reporting.

---

## Alle Lernpfade im Detail

- **[Lernpfad: Graphen & Bäume](roadmaps/graphs.md):** Repräsentation, Traversierung, Kürzeste Pfade, Euler-Tour und LCA.
- **[Lernpfad: Arrays, Strings & Sequenz-Muster](roadmaps/arrays-strings.md):** Two Pointers, Sliding Window, Sweep-Line und Binäre Suche.
- **[Lernpfad: Dynamische Programmierung (DP)](roadmaps/dynamic-programming.md):** Memoization, Tabulation, Knapsack und Zustandsräume.
- **[Lernpfad: Mathematik & Bit-Manipulation](roadmaps/math-bit-manipulation.md):** Bitmasken, XOR-Tricks, Zahlenspiegelung und Kalenderarithmetik.
- **[Lernpfad: Web Security & Bug Bounty](roadmaps/web-security.md):** Von HTTP-Grundlagen über Burp Suite bis hin zu OWASP Top 10 und Recon.

---

## Aufbau jeder Dokumentation

Jede Seite im Algodex folgt einem einheitlichen Standard:

1. **Intuition & Kernidee:** Bildhafte Erklärung des Algorithmus vor dem Code.
2. **Mermaid.js Diagramme:** Visuelle Veranschaulichung von Baumstrukturen, Graphen oder Zustandsautomaten.
3. **Python 3 Implementierung:** Sauber typisierter Code mit `typing` (`List`, `Tuple`, `Dict`, `Optional`) und Kommentaren.
4. **Komplexitätsanalyse:** Mathematisch präzise Aufschlüsselung von Zeit- ($\mathcal{O}(T)$) und Speicherbedarf ($\mathcal{O}(S)$).
5. **Edge Cases & Gotchas:** Aufzählung kritischer Randfälle (leere Eingaben, Duplikate, Rekursionslimits, Ganzzahlüberläufe).

---

## Navigation & Suche

Nutze die Seitenleiste links, das Glossar oder die Tastatur-Schnellsuche (<kbd>s</kbd> oder <kbd>/</kbd>), um direkt nach Algorithmen, Datenstrukturen oder LeetCode-IDs zu suchen.
