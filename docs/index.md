---
tags:
  - Übersicht
  - Home
  - Core
---

# FIER's Algodex

> Ein interaktives Entwickler-Wiki und Nachschlagewerk für **Algorithmen**, **Datenstrukturen** und **LeetCode-Lösungen in Python 3** – mit strikter Typisierung, mathematischen Komplexitätsanalysen und Diagrammen.

---

## Plattform-Übersicht

FIER's Wiki gliedert sich in zwei eigenständige, spezialisierte Fachbereiche:

| Bereich | Fokus & Themen | Einstiegspunkt |
| :--- | :--- | :--- |
| **FIER's Algodex** | Datenstrukturen, Algorithmen, Komplexität & LeetCode-Lösungen | [Startseite](index.md) (Aktuell hier) |
| **FIER's Red Algodex** | Web Security, PortSwigger-Techniken, OWASP Top 10 & Bug Bounties | [Red Algodex Startseite](red-algodex/index.md) |

---

## Schnellzugriff (Quick-Access Cards)

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

=== "Offensive Security (Red Algodex)"

    - **[Red Algodex Hub](red-algodex/index.md):** Der eigenständige Bereich für Penetration Testing und Bug Bounties.
    - **[Burp Suite Grundlagen](red-algodex/tools/burp-suite-basics.md):** Proxy, Repeater, Intruder und BApp Extensions (Autorize, Turbo Intruder).
    - **[Cross-Site Scripting (XSS)](red-algodex/vulnerabilities/xss.md):** Reflected, Stored und DOM-based XSS, Sources/Sinks und CSP.
    - **[SQL Injection (SQLi)](red-algodex/vulnerabilities/sqli.md):** Union-Based, Error-Based und Blind SQLi sowie Prepared Statements.
    - **[Server-Side Request Forgery (SSRF)](red-algodex/vulnerabilities/ssrf.md):** Cloud-Metadaten (AWS IMDS), Filter-Bypasses und OAST.
    - **[Broken Access Control & IDOR](red-algodex/vulnerabilities/access-control-idor.md):** Horizontale/vertikale Rechteausweitung und automatisierte Bypasses mit Autorize.

=== "Referenzen & Community"

    - **[Stichwort-Referenz (Keyword Index)](references.md):** Vollständiges alphabetisches Begriffsverzeichnis aller Algorithmen.
    - **[Changelog (What's New)](changelog.md):** Chronologische Übersicht über neue Algorithmen, Lernpfade und Features.
    - **[GitHub Repository](https://github.com/Fabian-dotcom/fiers-algodex):** Sourcecode, Issues und Beitragsrichtlinien.
    - **[GitHub Sponsor / Buy me a coffee](https://github.com/sponsors/Fabian-dotcom):** Unterstütze die Weiterentwicklung dieses Wikis.

---

## Die Lernpfade

Die detaillierten Checklisten und Stufenpläne findest du auf den jeweiligen Lernpfad-Seiten:

- **[Lernpfad: Graphen & Bäume](roadmaps/graphs.md):** Repräsentation (Adjazenzliste, Matrix, CSR), Traversierung (BFS/DFS), Kürzeste Pfade, Euler-Tour und LCA.
- **[Lernpfad: Arrays, Strings & Sequenz-Muster](roadmaps/arrays-strings.md):** Two Pointers, Sliding Window, Sweep-Line und Binäre Suche.
- **[Lernpfad: Dynamische Programmierung (DP)](roadmaps/dynamic-programming.md):** Memoization, Tabulation, Knapsack und Zustandsräume.
- **[Lernpfad: Mathematik & Bit-Manipulation](roadmaps/math-bit-manipulation.md):** Bitmasken, XOR-Tricks, Zahlenspiegelung und Kalenderarithmetik.
- **[Lernpfad: Web Security & Bug Bounty](red-algodex/roadmaps/web-security.md):** Chronologischer Stufenplan von HTTP-Basics über Burp Suite bis hin zu OWASP Top 10 und Recon.

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

Nutze die obere Tableiste zur Umschaltung zwischen **Core Algodex** und **Red Algodex**, die linke Seitenleiste zur Navigation oder die Tastatur-Schnellsuche (<kbd>s</kbd> oder <kbd>/</kbd>).
