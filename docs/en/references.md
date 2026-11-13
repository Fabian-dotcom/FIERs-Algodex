---
tags:
  - Referenz
  - Index
  - Glossar
---

# Begriffs- & Stichwort-Referenz (Keyword Index)

Diese Seite bietet eine strukturierte Übersicht aller Kernbegriffe, Datenstrukturen, Algorithmen und mathematischen Konzepte im Algodex mit ihren jeweiligen Zielseiten.

---

## Datenstrukturen

| Begriff / Stichworte | Erklärung | Dokumentation |
| :--- | :--- | :--- |
| **Adjazenzliste (Adjacency List)** | Dünne Graphspeicherung über Nachbar-Arrays $\mathcal{O}(V + E)$. | [Adjazenzliste](glossary/adjazenzliste.md) |
| **Adjazenzmatrix (Adjacency Matrix)** | Quadratische Matrix $V \times V$ für dichte Graphen und schnelle Kantenexistenz-Checks. | [Adjazenzmatrix](glossary/adjazenzmatrix.md) |
| **CSR-Format (Compressed Sparse Row)** | Flache, zusammenhängende 1D-Arrays (`row_ptr`, `targets`, `weights`) für maximale Cache-Lokalität. | [CSR-Format](glossary/csr-format.md) |
| **Hash Map / Hash Set / Dictionary** | Assoziative Speicherung mit amortisiert $\mathcal{O}(1)$-Zugriff. | [Hash Map & Hash Set](glossary/hash-map.md) |
| **Verkettete Liste (Linked List)** | Zeigerverkettete Knoten (`ListNode`), Dummy-Head-Pattern. | [Verkettete Liste](glossary/linked-list.md) |
| **Min-Heap / Priority Queue** | Vorrangswarteschlange für schnellen Zugriff auf das Minimum in $\mathcal{O}(1)$ und Einfügen in $\mathcal{O}(\log n)$. | [Min-Heap & Sweep-Line](glossary/min-heap-sweep-line.md) |
| **Two-Heap & Lazy Deletion** | Balancierte Max-/Min-Heaps für gleitende Mediane; ungültige Elemente werden per Häufigkeits-Tabelle markiert statt gesucht. | [Two-Heap & Lazy Deletion](glossary/two-heap-lazy-deletion.md) |
| **Median-Kosten (L1-Norm)** | $\sum \|a_i - \text{median}\|$ in $\mathcal{O}(1)$ über mitgeführte Half-Summen. | [Two-Heap & Lazy Deletion](glossary/two-heap-lazy-deletion.md) |
| **Fenwick-Baum (BIT / Binary Indexed Tree)** | Dynamische Präfixsummen und XOR-Aggregationen in $\mathcal{O}(\log n)$. | [Fortgeschrittene Baum-Techniken](glossary/advanced-tree-techniques.md) |

---

## Algorithmen & Traversierung

| Begriff / Stichworte | Erklärung | Dokumentation |
| :--- | :--- | :--- |
| **Tiefensuche (DFS / Depth-First Search)** | Geht Pfade bis zum Ende ab (Rekursion oder expliziter Stack). | [Tiefensuche & Breitensuche](glossary/traversierung-bfs-dfs.md) |
| **Breitensuche (BFS / Breadth-First Search)** | Schichtweise Erkundung via Queue für ungewichtete kürzeste Wege. | [Tiefensuche & Breitensuche](glossary/traversierung-bfs-dfs.md) |
| **Topologische Sortierung (Kahn-Algorithmus)** | Lineare Ordnung von Knoten in gerichteten, kreisfreien Graphen (DAGs). | [Topologische Sortierung](glossary/topologische-sortierung.md) |
| **Dijkstra / Zustandsbasierter Dijkstra** | Kürzeste Pfade mit Min-Heap und erweitertem Zustandsraum `(node, context)`. | [Zustandsbasierter Dijkstra](glossary/state-space-dijkstra.md) |
| **Zustandsraum-Reduktion** | Minimierung von Pfad-Historien auf essenzielle Invarianten (`letztes_zeichen`, `zaehler`). | [Zustandsbasierter Dijkstra](glossary/state-space-dijkstra.md) |
| **Flood Fill (Fluten)** | Zusammenhangskomponenten auf 2D-Gittern und Randeliminierung. | [Flood Fill & Gitter-Traversierung](glossary/flood-fill.md) |
| **Schiebefenster (Sliding Window)** | Dynamische und feste Intervalle mit Two-Pointers in $\mathcal{O}(n)$. | [Schiebefenster](glossary/sliding-window.md) |
| **Monotonic Stack with Cost Accumulation** | Backward sweep with monotonic stack, incremental costs, and a shrinking window for subarray repair costs. | [Monotonic Stack](glossary/monotonic-stack-cost-accumulation.md) |
| **Disjoint Set Union (Union-Find)** | `find`/`union` with path compression and union by size in almost $\mathcal{O}(1)$ ($\alpha(n)$) per operation. | [DSU / Union-Find](glossary/dsu-union-find.md) |
| **Binäre Suche (Binary Search)** | Logarithmische Suche $\mathcal{O}(\log n)$ und Partitionierung zweier sortierter Arrays. | [Binäre Suche](glossary/binary-search.md) |
| **Sweep-Line** | Ereignispunkt-Traversierung entlang einer Achse zur Intervallverarbeitung. | [Min-Heap & Sweep-Line](glossary/min-heap-sweep-line.md) |
| **Sortierte Abfragen & Zwei-Zeiger** | Offline-Abfragen mit Original-Index sortieren und mit zwei Zeigern monoton mitsweepen. | [Sortierte Abfragen & Zwei-Zeiger](glossary/sorted-queries-two-pointer.md) |
| **Event-Driven Simulation** | Frei-/Beschäftigt-Heaps und Zeitsprünge statt Sekunden-Tick in Scheduling-Problemen. | [Event-Driven Simulation](glossary/event-driven-simulation.md) |
| **Python Performance-Optimierungen** | Zero-Copy-Indexing statt Slicing, String-Allocation-Overhead und Built-in C-Speed. | [Python Performance](glossary/python-performance-optimization.md) |
| **Inversionszählung (Fenwick)** | Anzahl der Swaps beim Bubble-Sort-Sortieren in $\mathcal{O}(n \log n)$. | [Fortgeschrittene Baum-Techniken](glossary/advanced-tree-techniques.md) |
| **PageRank** | Zentralitätsbewertung im gerichteten Graphen via Random Walk und Power Iteration. | [PageRank](glossary/pagerank.md) |
| **Graph Neural Networks (GNN)** | Deep Learning auf Graphen durch Message Passing und Nachbarschafts-Aggregation. | [Graph Neural Networks](glossary/gnn.md) |
| **SciPy & Matrix-Vektor (SpMV)** | Dünnbesetzte Multiplikationen und wissenschaftliche Datenformate (CSR, CSC, COO). | [SciPy & Matrix-Vektor](glossary/scipy-matrix-vector.md) |
| **Speicher & Garbage Collection** | Cache-Lines, Pointer-Overhead, Referenzzählung und Stop-the-World GC. | [Speicherverwaltung & GC](glossary/memory-management.md) |

---

## Languages & Migration (Python → Rust)

| Term / Keywords | Explanation | Documentation |
| :--- | :--- | :--- |
| **Python ↔ Rust Translation** | Collection/iterator/error-handling equivalents: `deque` → `VecDeque`, `heapq` → `BinaryHeap`, exceptions → `Result`. | [Languages & Migration](glossary/languages-rust.md) |
| **Ownership & Borrowing** | Exactly one owner per value; `&T` reads, `&mut T` writes – deterministic instead of GC. | [Languages & Migration](glossary/languages-rust.md) |

---

## Baum-Spezialtechniken

| Begriff / Stichworte | Erklärung | Dokumentation |
| :--- | :--- | :--- |
| **LCA (Lowest Common Ancestor)** | Tiefster gemeinsamer Vorfahre zweier Baumknoten. | [Fortgeschrittene Baum-Techniken](glossary/advanced-tree-techniques.md) |
| **Binary Lifting** | Vorberechnung von $2^j$-Vorfahren für Baumsprünge in $\mathcal{O}(\log n)$. | [Fortgeschrittene Baum-Techniken](glossary/advanced-tree-techniques.md) |
| **Euler-Tour (Subtree Linearization)** | Abflachen eines Baumes in 1D-Intervalle $[\text{tin}, \text{tout}]$ via DFS. | [Fortgeschrittene Baum-Techniken](glossary/advanced-tree-techniques.md) |

---

## Mathematik, Bits & Komplexität

| Begriff / Stichworte | Erklärung | Dokumentation |
| :--- | :--- | :--- |
| **Landau-Symbole (Big-O Notation)** | Asymptotische Laufzeit- und Speicherkomplexität ($\mathcal{O}(1), \mathcal{O}(\log n), \dots$). | [Landau-Symbole & Big-O](glossary/o-notation.md) |
| **Ein-Pass durch algebraische Umformung** | Reduktion von Schleifen durch mathematische Summen-Umformung. | [Algebraische Ein-Pass-Optimierung](glossary/algebraic-one-pass.md) |
| **Speicherschonende Generatoren** | Lazy Evaluation in `sum()`, `min()`, `max()` für echten $\mathcal{O}(1)$-Speicherbedarf. | [Generator-Ausdrücke](glossary/generator-expressions.md) |
| **Constraint-Driven Design** | Asymmetrisch kleine Parametergrenzen als direkter Indikator für den Zielalgorithmus. | [Constraint-Driven Design](glossary/constraint-driven-design.md) |
| **Bitmasken & Bitweises XOR** | Kompakte Speicherung von Flags und Paritätsberechnungen in $\mathcal{O}(1)$. | [Bitweise Operationen](glossary/bit-manipulation.md) |
| **Palindrom-Bit-Trick** | Prüfung auf höchstens ein gesetztes Bit via `mask & (mask - 1) == 0`. | [Bitweise Operationen](glossary/bit-manipulation.md) |
| **Mathematische Zahlenumkehr** | Ziffernextraktion über Modulo/Division ohne String-Allokation. | [Mathematische Zahlenumkehr](glossary/math-number-reversal.md) |
| **Römische Zahlen** | Additive und subtraktive Konvertierung (Greedy & Rückwärts-Traversierung). | [Römische Zahlen](glossary/roman-numerals.md) |
| **Kalender- & Datumsarithmetik** | Gregorianische Schaltjahr-Regel und absolute Epochentage. | [Datums- & Kalender-Arithmetik](glossary/date-arithmetic.md) |
| **Zyklische Permutationen** | Invarianzprüfung zyklischer Verschiebungen und minimale Sortierzüge. | [Zyklische Permutationen](glossary/cyclic-permutations.md) |

---

## Web Security & Bug Bounty Hunting (Red Algodex)

| Begriff / Stichworte | Erklärung | Dokumentation |
| :--- | :--- | :--- |
| **Burp Suite (Proxy, Repeater, Intruder)** | Man-in-the-Middle HTTP-Proxy zum Abfangen, Manipulieren und Fuzzen von Web-Requests. | [Burp Suite Grundlagen](red-algodex/tools/burp-suite-basics.md) |
| **Web-Fundamente (HTTP, SOP, CORS, CSP)** | Browsergrenzen, Session-Sicherheit und Content Security Policies. | [Web-Fundamente](red-algodex/vulnerabilities/http-sop-cors-csp.md) |
| **Cross-Site Scripting (XSS)** | Clientseitige Code-Ausführung (Reflected, Stored, DOM) im Browser des Opfers. | [Cross-Site Scripting (XSS)](red-algodex/vulnerabilities/xss.md) |
| **Client-Side (CSRF, CORS, Clickjacking)** | Unbeabsichtigte Anfragen, Origin-Leaks und UI-Redressing. | [Client-Side Angriffe](red-algodex/vulnerabilities/client-side-advanced.md) |
| **SQL Injection (SQLi)** | Manipulation von Datenbankabfragen (Union, Error, Blind, Time-based) und Prepared Statements. | [SQL Injection (SQLi)](red-algodex/vulnerabilities/sqli.md) |
| **Server-Side Request Forgery (SSRF)** | Unautorisierte interne Requests durch den Webserver (Cloud-Metadaten, IMDS, OAST). | [Server-Side Request Forgery (SSRF)](red-algodex/vulnerabilities/ssrf.md) |
| **Broken Access Control & IDOR** | Fehlerhafte Berechtigungsprüfungen, Objekt-Level Autorisierung und Privilege Escalation. | [Broken Access Control & IDOR](red-algodex/vulnerabilities/access-control-idor.md) |
| **Command Injection & Path Traversal** | Ausführung von Shell-Befehlen und unbefugtes Auslesen von Systemdateien via `../`. | [Command Injection, Path Traversal & SSTI](red-algodex/vulnerabilities/command-injection-ssti.md) |
| **Server-Side Template Injection (SSTI)** | Codeausführung über Template-Engines (Jinja2, Twig, FreeMarker). | [Command Injection, Path Traversal & SSTI](red-algodex/vulnerabilities/command-injection-ssti.md) |
| **Business Logic Flaws** | Umgehung von Workflows, negative Preise und Coupon Stacking. | [Business Logic & JWT](red-algodex/vulnerabilities/business-logic-jwt.md) |
| **JWT-Schwachstellen** | `alg: none` Angriffe, schwache HMAC-Secrets und Algorithm Confusion. | [Business Logic & JWT](red-algodex/vulnerabilities/business-logic-jwt.md) |
| **HTTP Request Smuggling** | Desynchronisation zwischen Frontend-Proxy und Backend (CL.TE / TE.CL). | [Request Smuggling & Race Conditions](red-algodex/vulnerabilities/advanced-attacks.md) |
| **Race Conditions (TOCTOU)** | Gleichzeitige Anfragen und Single-Packet Attacks mit Turbo Intruder. | [Request Smuggling & Race Conditions](red-algodex/vulnerabilities/advanced-attacks.md) |
| **Bug Bounty Reconnaissance** | Asset Discovery, DNS Brute-Forcing, Content-Fuzzing (`ffuf`, `nuclei`) und CVSS-Reports. | [Reconnaissance & Reporting](red-algodex/tools/recon-reporting.md) |
