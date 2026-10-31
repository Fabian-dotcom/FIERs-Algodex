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
| **Binäre Suche (Binary Search)** | Logarithmische Suche $\mathcal{O}(\log n)$ und Partitionierung zweier sortierter Arrays. | [Binäre Suche](glossary/binary-search.md) |
| **Sweep-Line** | Ereignispunkt-Traversierung entlang einer Achse zur Intervallverarbeitung. | [Min-Heap & Sweep-Line](glossary/min-heap-sweep-line.md) |
| **PageRank** | Zentralitätsbewertung im gerichteten Graphen via Random Walk und Power Iteration. | [PageRank](glossary/pagerank.md) |
| **Graph Neural Networks (GNN)** | Deep Learning auf Graphen durch Message Passing und Nachbarschafts-Aggregation. | [Graph Neural Networks](glossary/gnn.md) |
| **SciPy & Matrix-Vektor (SpMV)** | Dünnbesetzte Multiplikationen und wissenschaftliche Datenformate (CSR, CSC, COO). | [SciPy & Matrix-Vektor](glossary/scipy-matrix-vector.md) |
| **Speicher & Garbage Collection** | Cache-Lines, Pointer-Overhead, Referenzzählung und Stop-the-World GC. | [Speicherverwaltung & GC](glossary/memory-management.md) |

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
| **Bitmasken & Bitweises XOR** | Kompakte Speicherung von Flags und Paritätsberechnungen in $\mathcal{O}(1)$. | [Bitweise Operationen](glossary/bit-manipulation.md) |
| **Palindrom-Bit-Trick** | Prüfung auf höchstens ein gesetztes Bit via `mask & (mask - 1) == 0`. | [Bitweise Operationen](glossary/bit-manipulation.md) |
| **Mathematische Zahlenumkehr** | Ziffernextraktion über Modulo/Division ohne String-Allokation. | [Mathematische Zahlenumkehr](glossary/math-number-reversal.md) |
| **Römische Zahlen** | Additive und subtraktive Konvertierung (Greedy & Rückwärts-Traversierung). | [Römische Zahlen](glossary/roman-numerals.md) |
| **Kalender- & Datumsarithmetik** | Gregorianische Schaltjahr-Regel und absolute Epochentage. | [Datums- & Kalender-Arithmetik](glossary/date-arithmetic.md) |
| **Zyklische Permutationen** | Invarianzprüfung zyklischer Verschiebungen und minimale Sortierzüge. | [Zyklische Permutationen](glossary/cyclic-permutations.md) |

---

## Web Security & Bug Bounty Hunting

| Begriff / Stichworte | Erklärung | Dokumentation |
| :--- | :--- | :--- |
| **Burp Suite (Proxy, Repeater, Intruder)** | Man-in-the-Middle HTTP-Proxy zum Abfangen, Manipulieren und Fuzzen von Web-Requests. | [Burp Suite Grundlagen](glossary/burp-suite-basics.md) |
| **Cross-Site Scripting (XSS)** | Clientseitige Code-Ausführung (Reflected, Stored, DOM) im Browser des Opfers. | [Cross-Site Scripting (XSS)](glossary/web-sec-xss.md) |
| **SQL Injection (SQLi)** | Manipulation von Datenbankabfragen (Union, Error, Blind, Time-based) und Prepared Statements. | [SQL Injection (SQLi)](glossary/web-sec-sqli.md) |
| **Server-Side Request Forgery (SSRF)** | Unautorisierte interne Requests durch den Webserver (Cloud-Metadaten, IMDS, OAST). | [Server-Side Request Forgery (SSRF)](glossary/web-sec-ssrf.md) |
| **Broken Access Control & IDOR** | Fehlerhafte Berechtigungsprüfungen, Objekt-Level Autorisierung und Privilege Escalation. | [Broken Access Control & IDOR](glossary/web-sec-access-control-idor.md) |
| **Command Injection & Path Traversal** | Ausführung von Shell-Befehlen und unbefugtes Auslesen von Systemdateien via `../`. | [Command Injection, Path Traversal & SSTI](glossary/web-sec-command-injection-ssti.md) |
| **Server-Side Template Injection (SSTI)** | Codeausführung über Template-Engines (Jinja2, Twig, FreeMarker). | [Command Injection, Path Traversal & SSTI](glossary/web-sec-command-injection-ssti.md) |
| **Business Logic Flaws** | Umgehung von Workflows, negative Preise und Coupon Stacking. | [Business Logic & JWT](glossary/web-sec-business-logic-jwt.md) |
| **JWT-Schwachstellen** | `alg: none` Angriffe, schwache HMAC-Secrets und Algorithm Confusion. | [Business Logic & JWT](glossary/web-sec-business-logic-jwt.md) |
| **HTTP Request Smuggling** | Desynchronisation zwischen Frontend-Proxy und Backend (CL.TE / TE.CL). | [Request Smuggling & Race Conditions](glossary/web-sec-advanced-attacks.md) |
| **Race Conditions (TOCTOU)** | Gleichzeitige Anfragen und Single-Packet Attacks mit Turbo Intruder. | [Request Smuggling & Race Conditions](glossary/web-sec-advanced-attacks.md) |
| **Bug Bounty Reconnaissance** | Asset Discovery, DNS Brute-Forcing, Content-Fuzzing (`ffuf`, `nuclei`) und CVSS-Reports. | [Reconnaissance & Reporting](glossary/web-sec-recon-reporting.md) |
