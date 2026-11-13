---
tags:
  - LeetCode
  - Array
  - String
  - Greedy
  - Sorting
  - Math
  - Medium
---

# LeetCode Weekly 526 Q1: Minimum Value of Merged Integers

- **Plattform:** Weekly Contest 526, Q1
- **Schwierigkeit:** Medium
- **Kategorien:** Array, String, Greedy, Sorting, Math
- **Verwandte Konzepte:** [String-Allocation Overhead](../glossary/python-performance-optimization.md)

---

## Aufgabenstellung

Gegeben ist ein Array `nums` gerader Länge $n$. Verschmelze die Elemente **paarweise in fester Reihenfolge**: `nums[0]` mit `nums[1]`, `nums[2]` mit `nums[3]`, usw. Die Verschmelzung zweier Zahlen hängt alle Dezimalziffern der ersten an die der zweiten an (Konkatenation).

Gib den **minimalen Wert** aller entstehenden verschmolzenen Zahlen zurück.

### Beispiele

```text
Input:  nums = [23, 55, 42, 21]
Output: 2142
Erklärung: Paare sind "2355", "4221". Das Minimum ist 2142 aus "42"+"21".
```

---

## Intuition & Lösungsansatz

### Optimierte Kernidee (lexikografischer Trick)

Konkatenierte Zahlen vergleicht man am besten als **Strings** — aber mit einem entscheidenden Detail: `(Länge, String)`-Tupel sind der richtige Vergleichsschlüssel, denn `"9" > "10"` lexikografisch, obwohl $9 > 10$ numerisch falsch herum sortiert. Erst die **Länge als Primärschlüssel** (kürzere Zahl ist immer kleiner, kein führender Nullfall da $\ge 1$) und dann der String-Vergleich bildet die numerische Ordnung korrekt ab.

1. `best` mit dem ersten Paar initialisieren.
2. Alle weiteren Paare mit `(len, string)` vergleichen und ggf. übernehmen.
3. Am Ende `int(best)` für den Rückgabewert.

Das läuft in $\mathcal{O}(n)$ Paar-Vergleichen und baut nur **eine** Zwischenzeichenkette je Schritt.

---

## Implementierung (Python 3)

```python
from typing import List


class Solution:
    def minMerged(self, nums: List[int]) -> int:
        """Findet den minimalen Wert aller fest-paarweise verschmolzenen Zahlen.

        Args:
            nums: Array gerader Länge

        Returns:
            Minimaler verschmolzener Wert
        """
        best = str(nums[0]) + str(nums[1])

        for i in range(2, len(nums), 2):
            merged = str(nums[i]) + str(nums[i + 1])
            # (Länge, String) bildet die numerische Ordnung korrekt ab
            if (len(merged), merged) < (len(best), best):
                best = merged

        return int(best)
```

---

## Komplexitätsanalyse

| Dimension                                            | Komplexität              | Begründung                                              |
| :--------------------------------------------------- | :----------------------- | :------------------------------------------------------ |
| **[Zeitkomplexität](../glossary/o-notation.md)**     | $\mathcal{O}(n \cdot d)$ | $n/2$ Paare, jeder Vergleich kostet bis zu $d$ Ziffern. |
| **[Speicherkomplexität](../glossary/o-notation.md)** | $\mathcal{O}(d)$         | Nur `best` und das aktuelle `merged` werden allokiert.  |

---

## Edge Cases & Fallstricke

- [x] **Reine String-Vergleiche sind falsch:** `"10" < "9"` lexikografisch — die Länge muss der Primärschlüssel sein.
- [x] **Feste Paarbildung:** Es darf umsortiert werden? Nein — die Paare stehen durch die Aufgabenstellung fest; nur der Minimalwert wird gesucht.
- [x] **Konkatenation statt Addition:** `str(a) + str(b)` nicht `a + b` verwechseln.
