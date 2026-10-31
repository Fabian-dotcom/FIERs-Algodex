<div align="center">

# FIER's Algodex

<p align="center">
  <strong>Ein modernes, interaktives Entwickler-Wiki für Algorithmen, Datenstrukturen, LeetCode-Lösungen in Python 3 & Offensive Web Security</strong>
</p>

<p align="center">
  <a href="https://github.com/Fabian-dotcom/fiers-algodex/actions"><img src="https://github.com/Fabian-dotcom/fiers-algodex/actions/workflows/deploy.yml/badge.svg" alt="Deploy Status" /></a>
  <a href="https://opensource.org/licenses/MIT"><img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="License: MIT" /></a>
  <a href="https://www.python.org/"><img src="https://img.shields.io/badge/Python-3.10+-3776AB.svg?logo=python&logoColor=white" alt="Python 3.10+" /></a>
  <a href="https://squidfunk.github.io/mkdocs-material/"><img src="https://img.shields.io/badge/Docs-MkDocs_Material-blue.svg" alt="MkDocs Material" /></a>
</p>

<p align="center">
  <a href="https://fabian-dotcom.github.io/fiers-algodex/"><strong>Hier geht es zur Live-Website</strong></a> |
  <a href="https://fabian-dotcom.github.io/fiers-algodex/red-algodex/"><strong>Red Algodex (Security Hub)</strong></a> |
  <a href="https://fabian-dotcom.github.io/fiers-algodex/references/"><strong>Stichwort-Referenz (A-Z)</strong></a>
</p>

<!-- Stylisches Banner -->
<svg viewBox="0 0 900 240" width="100%" max-width="900px" xmlns="http://www.w3.org/2000/svg" style="border-radius: 12px; margin: 1.5rem 0; box-shadow: 0 8px 30px rgba(0,0,0,0.35);">
  <defs>
    <linearGradient id="bgGrad" x1="0%" y1="0%" x2="100%" y2="100%">
      <stop offset="0%" stop-color="#0f111a"/>
      <stop offset="50%" stop-color="#1a1c2e"/>
      <stop offset="100%" stop-color="#2a1420"/>
    </linearGradient>
    <linearGradient id="accentCore" x1="0%" y1="0%" x2="100%" y2="0%">
      <stop offset="0%" stop-color="#3f51b5"/>
      <stop offset="100%" stop-color="#2196f3"/>
    </linearGradient>
    <linearGradient id="accentRed" x1="0%" y1="0%" x2="100%" y2="0%">
      <stop offset="0%" stop-color="#d32f2f"/>
      <stop offset="100%" stop-color="#ff5252"/>
    </linearGradient>
  </defs>

  <!-- Background -->
  <rect width="900" height="240" rx="12" fill="url(#bgGrad)" stroke="#30363d" stroke-width="2"/>

  <!-- Grid Pattern Overlay -->
  <g opacity="0.1" stroke="#ffffff" stroke-width="1">
    <line x1="100" y1="0" x2="100" y2="240"/>
    <line x1="200" y1="0" x2="200" y2="240"/>
    <line x1="300" y1="0" x2="300" y2="240"/>
    <line x1="400" y1="0" x2="400" y2="240"/>
    <line x1="500" y1="0" x2="500" y2="240"/>
    <line x1="600" y1="0" x2="600" y2="240"/>
    <line x1="700" y1="0" x2="700" y2="240"/>
    <line x1="800" y1="0" x2="800" y2="240"/>
    <line x1="0" y1="60" x2="900" y2="60"/>
    <line x1="0" y1="120" x2="900" y2="120"/>
    <line x1="0" y1="180" x2="900" y2="180"/>
  </g>

  <!-- Title & Subtitle -->
  <text x="450" y="85" text-anchor="middle" fill="#ffffff" font-family="-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif" font-size="38" font-weight="800" letter-spacing="1.5">
    FIER'S ALGODEX
  </text>
  <text x="450" y="125" text-anchor="middle" fill="#90a4ae" font-family="-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif" font-size="16" font-weight="400">
    Algorithmen, Datenstrukturen &amp; Offensive Security in Perfektion
  </text>

  <!-- Dual Badges / Hubs -->
  <!-- Core Algodex Badge -->
  <g transform="translate(180, 155)">
    <rect width="250" height="48" rx="8" fill="#1e2238" stroke="#3f51b5" stroke-width="1.5"/>
    <circle cx="28" cy="24" r="8" fill="#2196f3"/>
    <text x="48" y="24" fill="#ffffff" font-family="-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif" font-size="14" font-weight="700" dominant-baseline="middle">
      CORE ALGODEX
    </text>
    <text x="48" y="38" fill="#78909c" font-family="-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif" font-size="10">
      Python 3 • LeetCode • Big-O
    </text>
  </g>

  <!-- Red Algodex Badge -->
  <g transform="translate(470, 155)">
    <rect width="250" height="48" rx="8" fill="#2a1420" stroke="#d32f2f" stroke-width="1.5"/>
    <circle cx="28" cy="24" r="8" fill="#ff5252"/>
    <text x="48" y="24" fill="#ffffff" font-family="-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif" font-size="14" font-weight="700" dominant-baseline="middle">
      RED ALGODEX
    </text>
    <text x="48" y="38" fill="#b0bec5" font-family="-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif" font-size="10">
      Web Security • Bug Bounty • Burp
    </text>
  </g>
</svg>

</div>

---

## Plattform-Architektur: Zwei spezialisierte Hubs

FIER's Algodex trennt fundamentale Informatik und offensive Sicherheit sauber in zwei dedizierte Bereiche:

| Bereich | Themen & Inhalte | Link |
| :--- | :--- | :--- |
| **Core Algodex** | Datenstrukturen, Graphentheorie, Dynamische Programmierung & 18 LeetCode-Lösungen | [Live öffnen](https://fabian-dotcom.github.io/fiers-algodex/) |
| **Red Algodex** | PortSwigger-Labs, OWASP Top 10, Burp Suite Mastery, Reconnaissance & Bounties | [Live öffnen](https://fabian-dotcom.github.io/fiers-algodex/red-algodex/) |

---

## Highlights & Features

- **Strukturierte Lernpfade:** Von linearen Sequenzen über Graphen und Bäume bis hin zu dynamischer Programmierung und Web Security.
- **Sauberer Python 3 Code:** Alle Algorithmen nutzen strikte Type Hints (`typing`), anschauliche Variablennamen und ausführliche Inline-Kommentare.
- **Mathematische Komplexitätsanalysen:** Jede Seite enthält exakte Aufschlüsselungen für Zeit- ($\mathcal{O}(T)$) und Speicherkomplexität ($\mathcal{O}(S)$) mit interaktiver Big-O Sprungtabelle.
- **Interaktive Mermaid.js Visualisierungen:** Graphen, Baumstrukturen, Zustandsautomaten und Speicher-Layouts direkt im Browser gerendert.
- **High-Performance Architektur:** Detaillierte Betrachtungen zu Cache-Lokalität, CSR-Format, Garbage Collection und Pointer-Overhead.
- **Modernes Material-Theme:** Integrierter Dark Mode, Volltextsuche, Code-Copy-Buttons und interaktive Tabs.

---

## Vorzeige-Artikel & Einstiegspunkte

### Core Algodex (Informatik & Algorithmen)
- **[Zustandsbasierter Dijkstra (State-Space Dijkstra)](https://fabian-dotcom.github.io/fiers-algodex/glossary/state-space-dijkstra/):** Pfadsuche mit Historien und Zustandsraum-Reduktion in $\mathcal{O}((E \cdot S) \log(V \cdot S))$.
- **[CSR-Format (Compressed Sparse Row)](https://fabian-dotcom.github.io/fiers-algodex/glossary/csr-format/):** Flache 1D-Arrays für Graphen und Sparse-Matrizen zur Vermeidung von Pointer-Overhead.
- **[Landau-Symbole & Big-O Notation](https://fabian-dotcom.github.io/fiers-algodex/glossary/o-notation/):** Interaktiver SVG-Wachstumsvergleich und Sprungtabelle von $\mathcal{O}(1)$ bis $\mathcal{O}(n!)$.
- **[Fortgeschrittene Baum-Techniken](https://fabian-dotcom.github.io/fiers-algodex/glossary/advanced-tree-techniques/):** Lowest Common Ancestor (LCA) via Binary Lifting in $\mathcal{O}(\log n)$, Euler-Tour und Fenwick-Bäume.

### Red Algodex (Web Security & Bug Bounty)
- **[Lernpfad: Web Security & Bug Bounty Hunting](https://fabian-dotcom.github.io/fiers-algodex/red-algodex/roadmaps/web-security/):** Chronologischer Stufenplan von HTTP-Basics über Burp Suite bis hin zu OWASP Top 10 und Recon.
- **[Burp Suite Grundlagen & Proxy Mastery](https://fabian-dotcom.github.io/fiers-algodex/red-algodex/tools/burp-suite-basics/):** Intercept, Repeater, Intruder-Angriffstypen, Collaborator (OAST) und Autorize.
- **[Cross-Site Scripting (XSS)](https://fabian-dotcom.github.io/fiers-algodex/red-algodex/vulnerabilities/xss/):** Reflected, Stored und DOM-based XSS, Sources/Sinks und CSP.
- **[SQL Injection (SQLi)](https://fabian-dotcom.github.io/fiers-algodex/red-algodex/vulnerabilities/sqli/):** Union-Based, Error-Based, Blind SQLi (Boolean/Time) und Prepared Statements.
- **[Server-Side Request Forgery (SSRF)](https://fabian-dotcom.github.io/fiers-algodex/red-algodex/vulnerabilities/ssrf/):** Cloud-Metadaten (AWS IMDS), Filter-Bypasses und OAST.
- **[Broken Access Control & IDOR](https://fabian-dotcom.github.io/fiers-algodex/red-algodex/vulnerabilities/access-control-idor/):** Horizontale/vertikale Rechteausweitung und automatisierte Bypasses mit Autorize.

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
│   ├── index.md             # Startseite mit Hero-Section & geführten Einstiegspfaden
│   ├── references.md        # Zentraler A-Z Stichwort- und Keyword-Index
│   ├── changelog.md         # Chronologisches Änderungsprotokoll
│   ├── roadmaps/            # Strukturierte Lernpfade (Graphen, Arrays, DP, Mathe)
│   ├── glossary/            # Detaillierte Core-Konzepte (CSR, Dijkstra, Big-O, etc.)
│   ├── solutions/           # Vollständig dokumentierte LeetCode-Lösungen
│   ├── red-algodex/         # Eigenständiger Offensive Security & Bug Bounty Hub
│   │   ├── index.md         # Startseite des Security Hubs
│   │   ├── roadmaps/        # Web Security Stufenplan
│   │   ├── vulnerabilities/ # OWASP Top 10 Guides (XSS, SQLi, SSRF, IDOR, etc.)
│   │   └── tools/           # Burp Suite & Recon Pipeline
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

Wenn dir das Projekt gefällt oder weiterhilft, freue ich mich über einen Star auf GitHub.
