---
tags:
  - Meta
  - Changelog
  - Updates
---

# Changelog & Was ist neu?

Hier werden alle neuen Algorithmen, Datenstrukturen, LeetCode-Lösungen, Security-Konzepte und Plattform-Erweiterungen des Algodex chronologisch dokumentiert.

---

## 31. Oktober 2026

### Plattform-Architektur & UX-Relaunch
- **Interaktives Steuerzentrum auf der Startseite ([`docs/index.md`](index.md)):**  
  Hero-Section mit direkten Aktions-Buttons und vier geführten Einstiegspfaden (*Coding Interview Vorbereitung*, *Graphentheorie von 0 auf 100*, *Web Security Basics*, *Diskrete Mathematik & Bits*).
- **Entkopplung von FIER's Red Algodex ([`docs/red-algodex/`](red-algodex/index.md)):**  
  Vollständig eigenständiger Bereich für Offensive Security & Bug Bounty Hunting mit eigener Navigation, eigener Farbakzentuierung (`red-theme.css`) und klarer Trennung vom Algorithmen-Core.
- **Kategorisierte Sidebar & Material-Tabs in `mkdocs.yml`:**  
  Strukturierung des Glossars in aufklappbare Unterkategorien (*Graphentheorie*, *Lineare Strukturen & Suche*, *Diskrete Mathematik & Bits*, *System & Performance*).
- **Aussagekräftige GitHub README & Banner:**  
  Neues responsives SVG-Header-Banner für GitHub mit Direktverlinkung auf beide Live-Hubs und vollständiger Lösungsmatrix.

### Web Security & Bug Bounty (Red Algodex)
- **[Lernpfad: Web Security & Bug Bounty Hunting](red-algodex/roadmaps/web-security.md):** Chronologischer Lernweg von PortSwigger-Labs über OWASP Top 10 bis hin zu Reconnaissance.
- **[Burp Suite Grundlagen](red-algodex/tools/burp-suite-basics.md):** Proxy, Repeater, Intruder, Decoder, Collaborator und BApp Extensions (Autorize, Turbo Intruder).
- **[Web-Fundamente](red-algodex/vulnerabilities/http-sop-cors-csp.md):** HTTP/1.1 & HTTP/2, Cookie-Sicherheit (`HttpOnly`, `SameSite`), Same-Origin Policy (SOP), CORS und CSP.
- **[Client-Side Angriffe](red-algodex/vulnerabilities/client-side-advanced.md):** CSRF mit Auto-Submit PoCs, CORS Misconfigurations und Clickjacking via `<iframe>`.
- **[Cross-Site Scripting (XSS)](red-algodex/vulnerabilities/xss.md):** Reflected, Stored und DOM-based XSS, Sources/Sinks, WAF-Evasion und CSP.
- **[SQL Injection (SQLi)](red-algodex/vulnerabilities/sqli.md):** Union-Based, Error-Based, Blind SQLi (Boolean/Time) und Prepared Statements.
- **[Server-Side Request Forgery (SSRF)](red-algodex/vulnerabilities/ssrf.md):** Cloud-Metadaten (AWS IMDS), IP-Filter-Bypasses, DNS Rebinding und Blind SSRF.
- **[Broken Access Control & IDOR](red-algodex/vulnerabilities/access-control-idor.md):** Horizontale/vertikale Rechteausweitung und automatisierte IDOR-Erkennung mit Autorize.
- **[Command Injection, Path Traversal & SSTI](red-algodex/vulnerabilities/command-injection-ssti.md):** Shell-Injektionen, `/etc/passwd`-Traversal und Template-RCE.
- **[Business Logic & JWT-Schwachstellen](red-algodex/vulnerabilities/business-logic-jwt.md):** Logikfehler im Checkout, `alg: none` Angriffe und Key Confusion.
- **[Request Smuggling & Race Conditions](red-algodex/vulnerabilities/advanced-attacks.md):** CL.TE / TE.CL Desynchronisation und Single-Packet Attacks.
- **[Reconnaissance & Bug Bounty Reporting](red-algodex/tools/recon-reporting.md):** Asset Discovery (`subfinder`, `puredns`), Fuzzing (`ffuf`), `nuclei` und CVSS-Reports.

---

## 30. Oktober 2026

### Core Algorithmen & Datenstrukturen
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

### Core Lernpfade
- **[Lernpfad: Graphen & Bäume](roadmaps/graphs.md)**
- **[Lernpfad: Arrays, Strings & Sequenz-Muster](roadmaps/arrays-strings.md)**
- **[Lernpfad: Dynamische Programmierung (DP)](roadmaps/dynamic-programming.md)**
- **[Lernpfad: Mathematik & Bit-Manipulation](roadmaps/math-bit-manipulation.md)**

### Dokumentierte LeetCode-Lösungen
- 18 vollständig ausgearbeitete Lösungen inklusive Type Hints, Mermaid-Diagrammen und Komplexitätsanalysen (LC 1, 2, 3, 4, 9, 12, 13, 1254, 1360, 1851, 2409, 2791, 3619, 3644, 3841, 3942, 3963, 3970).
