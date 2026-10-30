# FIER's Algodex

> Ein modernes, interaktives Entwickler-Wiki für Algorithmen, Datenstrukturen & LeetCode-Lösungen in Python 3.

[![Deploy Status](https://github.com/Fabian-dotcom/FIERs-Algodex/actions/workflows/deploy.yml/badge.svg)](https://github.com/Fabian-dotcom/FIERs-Algodex/actions)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/)

[Hier geht's zur Live-Website](https://fabian-dotcom.github.io/fiers-algodex/)

---

## Übersicht & Live-Wiki

FIER's Algodex ist ein strukturiertes Nachschlagewerk für Coding-Interviews, algorithmische Wettbewerbe und Softwarearchitektur. Jedes Thema wird von der Grundidee über Diagramme bis hin zu typisierten Python-Implementierungen und Komplexitätsanalysen aufbereitet.

---

## Features

- **Strukturierte Lernpfade:** Von linearen Datenstrukturen über Graphen und Bäume bis hin zu dynamischer Programmierung und Bit-Manipulation.
- **Sauberer Python 3 Code:** Alle Lösungen nutzen strikte Type Hints (`typing`), anschauliche Variablennamen und ausführliche Inline-Kommentare.
- **Mathematische Komplexitätsanalysen:** Jede Seite enthält exakte Aufschlüsselungen für Zeit- ($\mathcal{O}(T)$) und Speicherkomplexität ($\mathcal{O}(S)$) mit interaktiver Big-O Sprungtabelle.
- **Interaktive Mermaid.js Visualisierungen:** Graphen, Baumstrukturen, Zustandsautomaten und Speicher-Layouts direkt im Browser gerendert.
- **High-Performance Architektur:** Detaillierte Betrachtungen zu Cache-Lokalität, CSR-Format, Garbage Collection und Pointer-Overhead.
- **Modernes Material-Theme:** Integrierter Dark Mode, Volltextsuche, Code-Copy-Buttons und interaktive Tabs.

---

## Themenübersicht & Lerninhalte

### Datenstrukturen & Graphen
- [x] **Adjazenzliste & Adjazenzmatrix:** Speicheroptimierung $\mathcal{O}(V + E)$ vs. $\mathcal{O}(V^2)$
- [x] **CSR-Format (Compressed Sparse Row):** Cache-effiziente 1D-Arrays für Graphen und Sparse-Matrizen
- [x] **Traversierung:** Breitensuche (BFS mit Queue) und iterative Tiefensuche (DFS mit manuellem Stack)
- [x] **Topologische Sortierung:** Kahn-Algorithmus mit In-Degree Queue und Zykluserkennung in DAGs
- [x] **Zustandsbasierter Dijkstra (State-Space Dijkstra):** Pfadsuche mit Historien und Zustandsraum-Reduktion
- [x] **Baum-Vorverarbeitung:** Lowest Common Ancestor (LCA) via Binary Lifting in $\mathcal{O}(\log n)$, Euler-Tour und Fenwick-Baum

### Lineare Sequenzen & Suche
- [x] **Hash Map & Hash Set:** $\mathcal{O}(1)$-Zugriff, Kollisionen und Two-Sum-Komplement-Muster
- [x] **Verkettete Listen:** Zeiger-Operationen, Sentinel/Dummy-Nodes und schriftliche Addition
- [x] **Schiebefenster (Sliding Window):** Dynamische und feste Intervalle in $\mathcal{O}(n)$, ASCII-Array-Tuning
- [x] **Binäre Suche:** Logarithmische Suche und Partitionierung zweier sortierter Arrays
- [x] **Min-Heap & Sweep-Line:** Prioritätswarteschlangen und Ereignispunktverarbeitung

### Diskrete Mathematik & Bit-Tricks
- [x] **Bitmasken & Bitweises XOR:** Paritätsprüfung und akkumulierendes Bit-AND
- [x] **Palindrom-Bit-Trick:** Prüfung auf maximal 1 gesetztes Bit via `mask & (mask - 1) == 0`
- [x] **Mathematische Zahlenumkehr:** Ziffernspiegelung ohne String-Konvertierung
- [x] **Römische Zahlen & Kalenderarithmetik:** Greedy-Zerlegung, Gregorianische Schaltjahresregeln und Epochentage

---

## Dokumentierte LeetCode-Lösungen

| ID | Titel | Schwierigkeit | Kernkonzepte |
| :---: | :--- | :---: | :--- |
| **1** | Two Sum | Easy | Hash Map, Komplement-Suche |
| **2** | Add Two Numbers | Medium | Linked List, Schriftliche Addition, Dummy Head |
| **3** | Longest Substring Without Repeating Characters | Medium | Sliding Window, Hash Map, ASCII-Array |
| **4** | Median of Two Sorted Arrays | Hard | Binary Search, Partitionierung |
| **9** | Palindrome Number | Easy | Mathematik, Ziffernspiegelung ohne String |
| **12** | Integer to Roman | Medium | Greedy-Tabelle, Stellenwert-Lookup |
| **13** | Roman to Integer | Easy | Rückwärts-Traversierung |
| **1254** | Number of Closed Islands | Medium | Flood Fill, Randeliminierung, Stack-DFS |
| **1360** | Number of Days Between Two Dates | Easy | Kalenderarithmetik, Schaltjahre |
| **1851** | Minimum Interval to Include Each Query | Hard | Sweep-Line, Min-Heap, Lazy Invalidation |
| **2409** | Count Days Spent Together | Easy | Intervall-Schnittmenge, Epochentage |
| **2791** | Count Paths That Can Form a Palindrome in a Tree | Hard | DFS, 26-Bit-Maske, Prefix-XOR |
| **3619** | Count Islands With Total Value Divisible by K | Medium | Iterative DFS, In-Place Fluten |
| **3644** | Maximum K to Sort a Permutation | Medium | Akkumulierendes Bit-AND, Permutationen |
| **3841** | Palindromic Path Queries in a Tree | Hard | Euler-Tour, Binary Lifting, Fenwick-Baum |
| **3942** | Minimum Operations to Sort a Permutation | Medium | Zyklische Permutationen, Shift & Reverse |
| **3963** | Create Grid With Exactly One Path | Medium | Konstruktives Matrix-Design |
| **3970** | Shortest Path With At Most K Consecutive Characters | Hard | Zustandsbasierter Dijkstra, Min-Heap |

---

## Repository-Struktur

```text
FIERs-Algodex/
├── docs/
│   ├── index.md             # Startseite mit interaktiver Roadmap & Quick-Access Cards
│   ├── references.md        # Zentraler Stichwort- und Keyword-Index
│   ├── changelog.md         # Chronologisches Änderungsprotokoll
│   ├── roadmaps/            # Strukturierte Lernpfade (Graphen, Arrays, DP, Mathe)
│   ├── glossary/            # Detaillierte Konzepte (CSR, Dijkstra, Big-O, etc.)
│   ├── solutions/           # Vollständig dokumentierte LeetCode-Lösungen
│   └── templates/           # Standardisiertes Markdown-Template für neue Lösungen
├── mkdocs.yml               # MkDocs Material Konfiguration
├── LICENSE                  # MIT-Lizenz
└── .github/workflows/       # Automatisches CI/CD Deployment auf GitHub Pages
```

---

## Lokale Entwicklung

Voraussetzung: Python 3.10+

```bash
# Repository klonen
git clone https://github.com/Fabian-dotcom/fiers-algodex.git
cd fiers-algodex

# MkDocs Material installieren
pip install mkdocs-material

# Lokalen Entwicklungsserver starten
mkdocs serve
```

Die Dokumentation ist anschließend unter `http://127.0.0.1:8000` im Browser erreichbar.

---

## Lizenz & Mitwirkung

Dieses Projekt steht unter der [MIT-Lizenz](LICENSE).  
Feedback, Korrekturen oder neue Aufgabenvorschläge sind herzlich willkommen. Eröffne gerne ein Issue oder erstelle einen Pull Request.

Wenn dir das Projekt hilft oder gefällt, freue ich mich über einen Star auf GitHub.
