---
tags:
  - Meta
  - Changelog
  - Updates
---

# Changelog & What's New?

Chronological log of all new algorithms, data structures, LeetCode solutions, security write-ups, and architectural improvements in Algodex.

---

## November 4, 2026

### Multi-Language Architecture (i18n)
- **Official Material Multi-Site Setup (German & English):**  
  Full bilingual deployment across `/de/` and `/en/`.
- **Completely Isolated Search Indices:**  
  Each language builds into its own site bundle with its own dedicated `search_index.json`. Searching in English returns zero duplicate German hits, and vice versa.
- **Native Header Language Selector:**  
  Toggle seamlessly between German and English via the top-right header language dropdown powered by `extra.alternate`.
- **Smart Root Redirect:**  
  Visitors to the root domain are automatically forwarded to `/de/` or `/en/` according to browser language preferences.

---

## October 31, 2026

### Platform Architecture & UX Relaunch
- **Interactive Control Center on Home:** Guided routes for interviews, graph theory, web security, and discrete math.
- **FIER's Red Algodex Decoupling:** Standalone offensive security and bug bounty hub with specialized dark-red branding.
- **Categorized Sidebar & Tabs:** Grouped glossary entries into collapsible sections.
- **SVG GitHub Header Banner:** Responsive vector banner for the repository homepage.

---

## October 30, 2026

### Core Algorithms & Concepts
- State-Space Dijkstra, CSR Format, PageRank, Graph Neural Networks, SpMV with SciPy, Memory Management, BFS/DFS, Topological Sort, Big-O Complexity Graph.
- 18 comprehensively documented LeetCode solutions (LC 1, 2, 3, 4, 9, 12, 13, 1254, 1360, 1851, 2409, 2791, 3619, 3644, 3841, 3942, 3963, 3970).
