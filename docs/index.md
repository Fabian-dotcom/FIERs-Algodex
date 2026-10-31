---
tags:
  - Übersicht
  - Home
  - Core
---

# FIER's Algodex

<div style="background: linear-gradient(135deg, #1e1e2f 0%, #25283d 100%); border: 1px solid #3f51b5; border-radius: 12px; padding: 1.8rem 2rem; margin: 1rem 0 2rem 0; box-shadow: 0 4px 20px rgba(0,0,0,0.25);">
  <h2 style="margin: 0 0 0.5rem 0; color: #ffffff; border: none; font-size: 1.5rem;">Willkommen im Steuerzentrum des Algodex</h2>
  <p style="margin: 0 0 1.2rem 0; color: #b0bec5; font-size: 1.05rem; line-height: 1.5;">
    Das interaktive Entwickler-Wiki für <strong>Algorithmen</strong>, <strong>Datenstrukturen</strong>, <strong>LeetCode-Lösungen in Python 3</strong> und <strong>Offensive Web Security</strong> – fundiert, präzise und in eigenen Worten.
  </p>
  <div style="display: flex; gap: 0.8rem; flex-wrap: wrap;">
    <a href="roadmaps/graphs.md" class="md-button md-button--primary" style="font-weight: bold; padding: 0.6rem 1.2rem; border-radius: 6px;">
      Core Algodex (Python & LeetCode)
    </a>
    <a href="red-algodex/index.md" class="md-button" style="background-color: #b71c1c; color: white; border: none; font-weight: bold; padding: 0.6rem 1.2rem; border-radius: 6px;">
      Red Algodex (Security Hub)
    </a>
    <a href="references.md" class="md-button" style="font-weight: bold; padding: 0.6rem 1.2rem; border-radius: 6px;">
      Stichwort-Referenz (A-Z)
    </a>
  </div>
</div>

---

## Strukturierte Einstiegspfade (Geführte Routen)

Wähle deinen passenden Pfad, um chronologisch und strukturiert durch die Inhalte geführt zu werden:

<div class="grid cards" markdown>

-   **Coding Interview Vorbereitung**

    ---

    Der kompakte Weg durch die unverzichtbaren Algorithmenmuster für technische Interviews.
    
    1. [Landau-Symbole & Big-O Notation](glossary/o-notation.md)
    2. [Hash Map & Two Sum Komplement](glossary/hash-map.md)
    3. [Schiebefenster (Sliding Window)](glossary/sliding-window.md)
    4. [Binäre Suche & Partitionierung](glossary/binary-search.md)
    
    [:octicons-arrow-right-24: Zum Lernpfad Arrays & Strings](roadmaps/arrays-strings.md)

-   **Graphentheorie & Bäume von 0 auf 100**

    ---

    Von der Speicherung im Speicher bis zu fortgeschrittenen Baum- und Pfadtechniken.
    
    1. [Adjazenzliste](glossary/adjazenzliste.md) & [CSR-Format](glossary/csr-format.md)
    2. [Graph-Traversierung (BFS & DFS)](glossary/traversierung-bfs-dfs.md)
    3. [Zustandsbasierter Dijkstra](glossary/state-space-dijkstra.md)
    4. [Binary Lifting & LCA](glossary/advanced-tree-techniques.md)
    
    [:octicons-arrow-right-24: Zum Lernpfad Graphen & Bäume](roadmaps/graphs.md)

-   **Web Security & Bug Bounty Basics**

    ---

    Einstieg in Offensive Security nach PortSwigger- und OWASP-Standards im Red Algodex.
    
    1. [Web-Fundamente (HTTP, SOP, CORS, CSP)](red-algodex/vulnerabilities/http-sop-cors-csp.md)
    2. [Burp Suite Grundlagen & Proxy Mastery](red-algodex/tools/burp-suite-basics.md)
    3. [Cross-Site Scripting (XSS)](red-algodex/vulnerabilities/xss.md)
    4. [SQL Injection (SQLi)](red-algodex/vulnerabilities/sqli.md)
    
    [:octicons-arrow-right-24: Zum Red Algodex Security Hub](red-algodex/index.md)

-   **Diskrete Mathematik & Bit-Tricks**

    ---

    Hocheffiziente Problemlösungen auf Byte-Ebene in extrem wenigen CPU-Zyklen.
    
    1. [Bitweise Operationen & Bitmasken](glossary/bit-manipulation.md)
    2. [Palindrom-Bit-Trick in O(1)](glossary/bit-manipulation.md)
    3. [Mathematische Zahlenumkehr](glossary/math-number-reversal.md)
    4. [Zyklische Permutationen](glossary/cyclic-permutations.md)
    
    [:octicons-arrow-right-24: Zum Lernpfad Mathematik & Bits](roadmaps/math-bit-manipulation.md)

</div>

---

## Schnellzugriff (Quick-Access)

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
