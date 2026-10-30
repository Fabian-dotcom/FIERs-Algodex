---
tags:
  - Math
  - Complexity
  - Theory
  - Big-O
---

# Landau-Symbole (Big-O Notation) & Komplexitätsanalyse

Die **Landau-Notation (Big-O)** beschreibt das asymptotische Wachstumsverhalten von Algorithmen bezüglich **Laufzeit** $\mathcal{O}(T)$ und **Speicherbedarf** $\mathcal{O}(S)$ bei wachsender Eingabegröße $n$.

---

## Grafischer Wachstumsvergleich

Das folgende Diagramm veranschaulicht, wie drastisch die benötigte Anzahl an Operationen bei wachsendem $n$ explodiert:

<div style="text-align: center; margin: 2rem 0;">
<svg viewBox="0 0 650 380" width="100%" max-width="650px" style="background: #1e1e24; border-radius: 8px; font-family: sans-serif;">
  <!-- Grid Lines -->
  <line x1="60" y1="320" x2="600" y2="320" stroke="#444" stroke-width="2"/>
  <line x1="60" y1="40" x2="60" y2="320" stroke="#444" stroke-width="2"/>
  <line x1="60" y1="250" x2="600" y2="250" stroke="#333" stroke-dasharray="4"/>
  <line x1="60" y1="180" x2="600" y2="180" stroke="#333" stroke-dasharray="4"/>
  <line x1="60" y1="110" x2="600" y2="110" stroke="#333" stroke-dasharray="4"/>
  
  <!-- Axis Labels -->
  <text x="310" y="355" fill="#aaa" font-size="13">Eingabegröße (n) →</text>
  <text x="20" y="180" fill="#aaa" font-size="13" transform="rotate(-90 20 180)">Operationen / Zeit →</text>
  
  <!-- Curves -->
  <!-- O(1) -->
  <line x1="60" y1="310" x2="580" y2="310" stroke="#4caf50" stroke-width="3"/>
  <text x="590" y="314" fill="#4caf50" font-size="12" font-weight="bold">O(1)</text>
  
  <!-- O(log n) -->
  <path d="M 60 310 Q 150 295 300 285 T 580 275" fill="none" stroke="#8bc34a" stroke-width="3"/>
  <text x="590" y="278" fill="#8bc34a" font-size="12" font-weight="bold">O(log n)</text>
  
  <!-- O(n) -->
  <line x1="60" y1="310" x2="560" y2="200" stroke="#cddc39" stroke-width="3"/>
  <text x="570" y="200" fill="#cddc39" font-size="12" font-weight="bold">O(n)</text>
  
  <!-- O(n log n) -->
  <path d="M 60 310 Q 300 240 500 130" fill="none" stroke="#ffeb3b" stroke-width="3"/>
  <text x="510" y="130" fill="#ffeb3b" font-size="12" font-weight="bold">O(n log n)</text>
  
  <!-- O(n^2) -->
  <path d="M 60 310 Q 250 280 360 60" fill="none" stroke="#ff9800" stroke-width="3"/>
  <text x="370" y="65" fill="#ff9800" font-size="12" font-weight="bold">O(n²)</text>
  
  <!-- O(2^n) -->
  <path d="M 60 310 Q 160 300 210 50" fill="none" stroke="#f44336" stroke-width="3"/>
  <text x="215" y="55" fill="#f44336" font-size="12" font-weight="bold">O(2ⁿ)</text>
  
  <!-- O(n!) -->
  <path d="M 60 310 Q 110 290 130 50" fill="none" stroke="#b71c1c" stroke-width="3"/>
  <text x="135" y="55" fill="#b71c1c" font-size="12" font-weight="bold">O(n!)</text>
</svg>
</div>

---

## Interaktive Übersicht der Komplexitätsklassen

Klicke auf eine Klasse, um direkt zur detaillierten Erklärung und Beispielen zu springen:

| Klasse | Bezeichnung | Bewertung | Typische Datenstrukturen / Algorithmen |
| :--- | :--- | :--- | :--- |
| [<span id="nav-o1">**$\mathcal{O}(1)$**</span>](#1-o1-konstanter-aufwand) | Konstanter Aufwand | Exzellent | Array-Index, Hash-Lookup, Bit-Operationen |
| [<span id="nav-ologn">**$\mathcal{O}(\log n)$**</span>](#2-olog-n-logarithmischer-aufwand) | Logarithmischer Aufwand | Sehr gut | [Binäre Suche](binary-search.md), [LCA mit Binary Lifting](advanced-tree-techniques.md), Heap-Push/Pop |
| [<span id="nav-on">**$\mathcal{O}(n)$**</span>](#3-on-linearer-aufwand) | Linearer Aufwand | Gut | [Sliding Window](sliding-window.md), Two Pointers, [Two Sum](hash-map.md) |
| [<span id="nav-ove">**$\mathcal{O}(V + E)$**</span>](#4-ov--e-linear-auf-graphen) | Linear auf Graphen | Gut | [Tiefensuche (DFS)](traversierung-bfs-dfs.md), [Breitensuche (BFS)](traversierung-bfs-dfs.md), [Topologische Sortierung](topologische-sortierung.md) |
| [<span id="nav-onlogn">**$\mathcal{O}(n \log n)$**</span>](#5-on-log-n-linearithmischer-aufwand) | Linearithmischer Aufwand | Akzeptabel | MergeSort, TimSort, Sweep-Line mit [Min-Heap](min-heap-sweep-line.md) |
| [<span id="nav-odijkstra">**$\mathcal{O}((V + E) \log V)$**</span>](#6-ov--e-log-v-krzeste-pfade) | Kürzeste Pfade | Gut | Dijkstra mit Priority Queue, [Zustandsbasierter Dijkstra](state-space-dijkstra.md) |
| [<span id="nav-on2">**$\mathcal{O}(n^2)$ bzw. $\mathcal{O}(V^2)$**</span>](#7-on2-bzw-ov2-quadratischer-aufwand) | Quadratischer Aufwand | Kritisch bei $n > 10^4$ | Verschachtelte Schleifen, [Adjazenzmatrix](adjazenzmatrix.md), Floyd-Warshall |
| [<span id="nav-o2n">**$\mathcal{O}(2^n)$ und $\mathcal{O}(n!)$**</span>](#8-o2n-und-on-exponentiell--faktoriell) | Exponentiell / Faktoriell | Nur für kleine $n$ | Alle Teilmengen (Bitmask-DP), Permutationen, TSP |

---

## Die wichtigsten Klassen im Detail

### 1. $\mathcal{O}(1)$ – Konstanter Aufwand
Unabhängig von der Eingabegröße benötigt die Operation immer denselben konstanten Aufwand.
- **Beispiele:** Array-Indexzugriff (`arr[i]`), [Hash Map](hash-map.md)-Lookup im Durchschnitt (`dict[key]`), `heapq.heappop`-Spitze ansehen (`heap[0]`), Bitweise Operationen (`x & (x - 1)`).

### 2. $\mathcal{O}(\log n)$ – Logarithmischer Aufwand
In jedem Schritt wird der verbleibende Suchraum um einen festen Faktor halbiert.
- **Beispiele:** [Binäre Suche](binary-search.md), [LCA mit Binary Lifting](advanced-tree-techniques.md), Einfügen/Löschen in einem [Min-Heap](min-heap-sweep-line.md), Abfragen im [Fenwick-Baum](advanced-tree-techniques.md).

### 3. $\mathcal{O}(n)$ – Linearer Aufwand
Jedes Element der Eingabe wird eine konstante Anzahl von Malen betrachtet.
- **Beispiele:** Lineare Suche, [Schiebefenster (Sliding Window)](sliding-window.md), [Two Sum mit Hash Map](hash-map.md), [Zyklische Permutationsprüfung](cyclic-permutations.md).

### 4. $\mathcal{O}(V + E)$ – Linear auf Graphen
Jeder Knoten $V$ und jede Kante $E$ wird höchstens eine feste Anzahl von Malen traversiert.
- **Beispiele:** [Tiefensuche (DFS) und Breitensuche (BFS)](traversierung-bfs-dfs.md), [Topologische Sortierung](topologische-sortierung.md), [Flood Fill](flood-fill.md), Traversierung im [CSR-Format](csr-format.md).

### 5. $\mathcal{O}(n \log n)$ – Linearithmischer Aufwand
Typisch für vergleichsbasierte Sortierverfahren oder Algorithmen, die für $n$ Elemente jeweils eine $\mathcal{O}(\log n)$-Datenstruktur befragen.
- **Beispiele:** MergeSort, TimSort (Pythons `sort()`), [Sweep-Line](min-heap-sweep-line.md) mit Min-Heap ([LeetCode 1851](../solutions/leetcode-1851.md)).

### 6. $\mathcal{O}((V + E) \log V)$ – Kürzeste Pfade
Dijkstra mit Min-Heap / Priority Queue. Im [zustandsbasierten Dijkstra](state-space-dijkstra.md) skaliert dies zu $\mathcal{O}((E \cdot S) \log(V \cdot S))$.

### 7. $\mathcal{O}(n^2)$ bzw. $\mathcal{O}(V^2)$ – Quadratischer Aufwand
In der Regel verschachtelte Schleifen über die gesamte Eingabe.
- **Beispiele:** Naive Brute-Force-Paarsuchen, Bubble Sort, [Adjazenzmatrix-Initialisierung](adjazenzmatrix.md). Bei $n > 10^4$ führt dies im Coding-Interview fast immer zu *Time Limit Exceeded (TLE)*.

### 8. $\mathcal{O}(2^n)$ und $\mathcal{O}(n!)$ – Exponentiell / Faktoriell
- **Beispiele:** Erzeugen aller Teilmengen ($2^n$), Erzeugen aller Permutationen ($n!$), Traveling Salesperson Problem (Brute Force).

---

## Faustregel für Wettbewerbe & Interviews

In der Regel hat ein System ein Limit von ca. $10^7$ bis $10^8$ Operationen pro Sekunde:

| Eingabegröße $n$ | Maximal akzeptable Komplexität | Typische Lösungsansätze |
| :--- | :--- | :--- |
| $n \le 12$ | $\mathcal{O}(n!)$ oder $\mathcal{O}(2^n \cdot n^2)$ | Permutationen, TSP, Backtracking |
| $n \le 20$ | $\mathcal{O}(2^n)$ oder $\mathcal{O}(2^n \cdot n)$ | Bitmask-DP, Backtracking |
| $n \le 10^3$ | $\mathcal{O}(n^2)$ | 2D Dynamic Programming, Matrix-Traversierung |
| $n \le 10^5$ | $\mathcal{O}(n \log n)$ oder $\mathcal{O}(n)$ | Sortieren, Heap, Sweep-Line, [Binary Search](binary-search.md), Two Pointers |
| $n \le 10^7$ | $\mathcal{O}(n)$ oder $\mathcal{O}(\log n)$ | [Sliding Window](sliding-window.md), Prefix-Summen, [Hash Maps](hash-map.md) |
| $n \ge 10^9$ | $\mathcal{O}(\log n)$ oder $\mathcal{O}(1)$ | Reine Mathematik, Modulo-Arithmetik, Matrix-Exponentiation |
