---
tags:
  - LeetCode
  - Matrix
  - Constructive
  - Medium
---



# LeetCode 3963: Create Grid With Exactly One Path

- **Plattform:** [LeetCode #3963](https://leetcode.com/problems/create-grid-with-exactly-one-path/)
- **Schwierigkeit:** Medium
- **Kategorien:** Matrix, Constructive Algorithms, Grid
- **Verwandte Konzepte:** [Flood Fill & Gitter-Traversierung](../glossary/flood-fill.md)

---

## Aufgabenstellung

Gegeben sind zwei positive Ganzzahlen $m$ (Zeilen) und $n$ (Spalten).

Konstruiere ein 2D-Gitter der Dimension $m \times n$, bestehend aus begehbaren Feldern (`'.'`) und Hindernissen (`'#'`), sodass:
1. Das Startfeld $(0, 0)$ und das Zielfeld $(m-1, n-1)$ begehbar sind.
2. Es **genau einen einzigen einfachen Pfad** (durch orthogonale Schritte) von $(0, 0)$ nach $(m-1, n-1)$ gibt.

Gib das konstruierte Gitter als Liste von Zeichenketten (Zeilen) zurück.

### Beispiele

```text
Input:  m = 2, n = 3
Output: [
  ".##",
  "..."
]
Erklärung: 
Start bei (0, 0). Da (0, 1) und (0, 2) Wände '#' sind, muss man nach unten zu (1, 0) gehen 
und dann geradeaus entlang der letzten Zeile zu (1, 2). Es existiert genau dieser eine Weg.
```

---

## Intuition & Lösungsansatz

### 1. Konstruktives Design
Ein einfaches Gitter mit genau einem Pfad lässt sich deterministisch konstruieren, indem fast alle Felder durch Wände (`'#'`) blockiert werden und nur eine einzige zwingende Schneise von $(0, 0)$ zum Ziel offen bleibt:

- Initialisiere das gesamte $m \times n$ Gitter mit Hindernissen `'#'`.
- Setze die erste Spalte oder Zeile so, dass nur ein einziger Ausgang möglich ist:
  - Startfeld $(0, 0) = \text{'.'}$.
  - Wenn wir die gesamte Spalte $0$ von $(0, 0)$ bis $(m-1, 0)$ öffnen und anschließend die letzte Zeile $m-1$ von $(m-1, 0)$ bis $(m-1, n-1)$ öffnen, gibt es genau einen Pfad in L-Form.
- Bei kleineren Gittern (wie $m=2, n=3$):
  - Zeile $0$: `['.', '#', '#', ...]`
  - Zeile $m-1$: `['.', '.', '.', ...]`
  - Alle Zwischenzeilen $1 \dots m-2$ haben nur in Spalte $0$ einen Punkt `'.'`.

```text
. # # #
. # # #
. . . .  <- Ziel bei (m-1, n-1)
```

Da jede Abzweigung durch `'#'` blockiert ist, hat jeder Schritt auf dem Pfad genau eine zulässige Fortsetzung.

---

## Implementierung (Python 3)

```python
from typing import List


class Solution:
    def solve(self, m: int, n: int) -> List[str]:
        """Konstruiert ein m x n Gitter mit exakt einem Pfad von (0, 0) nach (m-1, n-1).

        Args:
            m: Anzahl Zeilen
            n: Anzahl Spalten

        Returns:
            Liste von Zeilen-Strings
        """
        # Gitter komplett mit Hindernissen '#' initialisieren
        grid = [["#"] * n for _ in range(m)]

        # 1. Pfad entlang der ersten Spalte nach unten öffnen
        for r in range(m):
            grid[r][0] = "."

        # 2. Pfad entlang der letzten Zeile nach rechts zum Ziel öffnen
        for c in range(n):
            grid[m - 1][c] = "."

        return ["".join(row) for row in grid]
```

---

## Komplexitätsanalyse

| Dimension | Komplexität | Begründung |
| :--- | :--- | :--- |
| **[Zeitkomplexität](../glossary/o-notation.md)** | $\mathcal{O}(m \cdot n)$ | Initialisieren und Konvertieren der Matrix der Größe $m \times n$ in Strings. |
| **[Speicherkomplexität](../glossary/o-notation.md)** | $\mathcal{O}(m \cdot n)$ | Speicherplatz für das konstruierte Gitter. |

---

## Edge Cases & Fallstricke

- [x] **Vermeidung von Referenz-Kopien:** Bei `[["#"] * n] * m` in Python teilen sich alle Zeilen dieselbe Listen-Referenz. Zwingend List Comprehension `[["#"] * n for _ in range(m)]` verwenden!
- [x] **$m = 1$ oder $n = 1$:** Bildet eine einfache Gerade aus Punkten ohne Verzweigungsmöglichkeit.
