---
tags:
  - LeetCode
  - Array
  - Math
  - Greedy
  - Easy
---

# LeetCode 3736: Minimum Moves to Equal Array Elements III

- **Plattform:** [LeetCode #3736](https://leetcode.com/problems/minimum-moves-to-equal-array-elements-iii/)
- **Schwierigkeit:** Easy
- **Kategorien:** Array, Math, Greedy
- **Verwandte Konzepte:** [Ein-Pass durch algebraische Umformung](../glossary/algebraic-one-pass.md) | [Speicherschonende Generatoren](../glossary/generator-expressions.md) | [LeetCode 453](leetcode-453.md)

---

## Aufgabenstellung

Gegeben ist ein Array `nums` der Länge $n$. In einem Zug darf **ein** Element um $1$ **erhöht** werden. Gib die minimale Zugzahl zurück, bis alle Elemente gleich sind.

### Beispiele

```text
Input:  nums = [2, 1, 3]
Output: 3
Erklärung: [2,1,3] → [2,2,3] → [2,3,3] → [3,3,3].
```

---

## Intuition & Lösungsansatz

### Optimierte Kernidee (nur Aufwärtzüge → Ziel ist das Maximum)

Da Elemente **nur erhöht** werden dürfen, muss jeder Wert bis zum **Maximum** $\max$ angehoben werden. Die Gesamtzugzahl ist damit die Summe aller Differenzen zum Maximum:

$$\text{moves} = \sum_{i} (\max - \text{nums}[i]) = n \cdot \max - \sum \text{nums}$$

Das ist die [algebraische Ein-Pass-Formel](../glossary/algebraic-one-pass.md) mit invertiertem Vorzeichen gegenüber [LeetCode 453](leetcode-453.md) — dort liegt das Ziel beim Minimum, weil $n-1$ Elemente gleichzeitig wachsen.

---

## Implementierung (Python 3)

```python
from typing import List


class Solution:
    def minMoves(self, nums: List[int]) -> int:
        """Zählt die minimalen Züge, bis alle Elemente gleich sind.

        Args:
            nums: Eingabearray

        Returns:
            Minimale Zugzahl
        """
        # Gesamt-Differenz aller Elemente zum größten Element.
        # max() und sum() laufen als Built-ins in C-Geschwindigkeit.
        max_val = max(nums)
        return len(nums) * max_val - sum(nums)
```

---

## Komplexitätsanalyse

| Dimension                                            | Komplexität      | Begründung                                                    |
| :--------------------------------------------------- | :--------------- | :------------------------------------------------------------ |
| **[Zeitkomplexität](../glossary/o-notation.md)**     | $\mathcal{O}(n)$ | `max()` und `sum()` durchlaufen die Liste einmal linear in C. |
| **[Speicherkomplexität](../glossary/o-notation.md)** | $\mathcal{O}(1)$ | Kein zusätzlicher, mitwachsender Speicher — nur Skalare.      |

---

## Edge Cases & Fallstricke

- [x] **Alle Elemente bereits gleich:** $n \cdot \max - \sum = 0$ — korrekt.
- [x] **Negative Zahlen:** Die Formel bleibt unverändert gültig, da sie nur Differenzen verwendet.
- [x] **Abgrenzung zu LeetCode 453:** Wächst pro Zug nur **ein** Element → Ziel ist `max`. Wachsen pro Zug $n-1$ Elemente → Ziel ist `min`. Die Perspektiv-Inversion ist der Schlüssel zu beiden geschlossenen Formeln.
