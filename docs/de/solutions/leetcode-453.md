---
tags:
  - LeetCode
  - Array
  - Math
  - Greedy
  - Easy
---

# LeetCode 453: Minimum Moves to Equal Array Elements

- **Plattform:** [LeetCode #453](https://leetcode.com/problems/minimum-moves-to-equal-array-elements/)
- **Schwierigkeit:** Easy
- **Kategorien:** Array, Math, Greedy
- **Verwandte Konzepte:** [Ein-Pass durch algebraische Umformung](../glossary/algebraic-one-pass.md) | [Speicherschonende Generatoren](../glossary/generator-expressions.md)

---

## Aufgabenstellung

Gegeben ist ein Array `nums` der Länge $n$. In einem Zug dürfen **$n - 1$ Elemente** um $1$ erhöht werden. Gib die minimale Zugzahl zurück, bis alle Elemente gleich sind.

### Beispiele

```text
Input:  nums = [1, 2, 3]
Output: 3
Erklärung: [1,2,3] → [2,3,3] → [3,4,3] → [3,3,3] (bzw. äquivalente Zugfolge).
```

---

## Intuition & Lösungsansatz

### 1. Naive Idee

Simuliere die Züge direkt und erhöhe in jedem Zug die $n-1$ kleinsten Elemente.

- Richtig, aber $\mathcal{O}(n \cdot m)$ — bei großen Wertebereichen inakzeptabel.

### 2. Optimierte Kernidee (Inversion der Perspektive)

Erhöhen von $n-1$ Elementen um 1 ist **relativ identisch** dazu, **ein** Element um 1 zu senken: relative Abstände ändern sich beim Erhöhen von $n-1$ Elementen nicht gegenüber dem Senken des einen übrig gebliebenen Elements.

Ziel: Alle Elemente auf das **Minimum** $\min$ herunterbringen. Die benötigten Züge sind:

$$\text{moves} = \sum_{i} (\text{nums}[i] - \min) = \sum \text{nums} - n \cdot \min$$

Die geschlossene Formel([Ein-Pass-Optimierung](../glossary/algebraic-one-pass.md)) liefert die Antwort in $\mathcal{O}(n)$ Zeit und $\mathcal{O}(1)$ Speicher.

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
        # Generator-Ausdrücke: O(n) Zeit, O(1) zusätzlicher Speicher,
        # laufen in C-Geschwindigkeit über die eingebauten Funktionen.
        return sum(nums) - len(nums) * min(nums)
```

---

## Komplexitätsanalyse

| Dimension                                            | Komplexität      | Begründung                                                                                           |
| :--------------------------------------------------- | :--------------- | :--------------------------------------------------------------------------------------------------- |
| **[Zeitkomplexität](../glossary/o-notation.md)**     | $\mathcal{O}(n)$ | `sum()` und `min()` durchlaufen die Liste einmal in C.                                               |
| **[Speicherkomplexität](../glossary/o-notation.md)** | $\mathcal{O}(1)$ | Generator-Ausdrücke bauen keine Zwischenliste auf ([Details](../glossary/generator-expressions.md)). |

---

## Edge Cases & Fallstricke

- [x] **Alle Elemente bereits gleich:** $\sum - n \cdot \min = 0$ — korrekt.
- [x] **Negative Zahlen:** Die Formel funktioniert unverändert, da sie nur auf Differenzen arbeitet.
- [x] **Verwandte Aufgabe:** Für increment-only-Züge auf **allen** $n$ Elementen siehe [LeetCode 3736](leetcode-3736.md) — dort ist das Maximum statt des Minimums das Ziel.
