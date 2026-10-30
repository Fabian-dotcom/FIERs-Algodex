---
tags:
  - LeetCode
  - Array
  - Binary Search
  - Divide and Conquer
  - Hard
---



# LeetCode 4: Median of Two Sorted Arrays

- **Plattform:** [LeetCode #4](https://leetcode.com/problems/median-of-two-sorted-arrays/)
- **Schwierigkeit:** Hard
- **Kategorien:** Array, [Binary Search](../glossary/binary-search.md), Divide and Conquer
- **Verwandte Konzepte:** [Binäre Suche](../glossary/binary-search.md)

---

## Aufgabenstellung

Gegeben sind zwei sortierte Arrays `nums1` und `nums2` der Größen $m$ und $n$.

Finde den **Median** der beiden sortierten Arrays. Die Gesamtlaufzeit muss in **$\mathcal{O}(\log(m + n))$** liegen.

### Beispiele

```text
Input:  nums1 = [1, 3], nums2 = [2]
Output: 2.0
Erklärung: Zusammengeführt [1, 2, 3], der Median ist 2.0.

Input:  nums1 = [1, 2], nums2 = [3, 4]
Output: 2.5
Erklärung: Zusammengeführt [1, 2, 3, 4], der Median ist (2 + 3) / 2 = 2.5.
```

---

## Intuition & Lösungsansatz

### 1. Naive Idee (Merge)
Führe beide Arrays wie im Merge-Schritt von MergeSort zusammen und nimm das mittlere Element.
- Laufzeit: $\mathcal{O}(m + n)$
- Speicher: $\mathcal{O}(m + n)$
- Problem: Erfüllt nicht die strikte Bedingung von $\mathcal{O}(\log(m + n))$.

### 2. Optimierte Kernidee (Binäre Suche auf der Partitionierung)
Der Median teilt eine sortierte Sequenz in zwei gleich große Hälften: eine linke Hälfte mit kleineren Elementen und eine rechte Hälfte mit größeren Elementen.

Wir müssen die beiden Arrays nicht physisch mergen. Es reicht, an den richtigen Stellen $i_1$ (in `nums1`) und $i_2$ (in `nums2`) Schnitte zu setzen:
- Linke Seite: enthält $i_1$ Elemente aus `nums1` und $i_2$ Elemente aus `nums2`.
- Gesamtzahl links: $\lfloor (m + n + 1) / 2 \rfloor$.

Sobald $i_1$ gewählt ist, steht $i_2$ fest:
$$i_2 = \frac{m + n + 1}{2} - i_1$$

Wir führen die [binäre Suche](../glossary/binary-search.md) nur auf dem **kürzeren Array** durch (falls $m > n$, tauschen wir `nums1` und `nums2`), sodass der Suchbereich $[0, m]$ minimal ist.

```text
Array 1:  ... links1  |  rechts1 ...
Array 2:  ... links2  |  rechts2 ...
```

Die Partitionierung ist genau dann korrekt, wenn:
$$\text{links}_1 \le \text{rechts}_2 \quad \text{und} \quad \text{links}_2 \le \text{rechts}_1$$

- Ist $\text{links}_1 > \text{rechts}_2$: Der Schnitt in `nums1` war zu weit rechts $\to \text{right} = i_1 - 1$.
- Ist $\text{links}_2 > \text{rechts}_1$: Der Schnitt in `nums1` war zu weit links $\to \text{left} = i_1 + 1$.

Liegt ein Schnitt am Rand (z. B. $i_1 = 0$), setzen wir $\text{links}_1 = -\infty$ bzw. $\text{rechts}_1 = +\infty$.

---

## Implementierung (Python 3)

```python
from typing import List


class Solution:
    def findMedianSortedArrays(
        self, nums1: List[int], nums2: List[int]
    ) -> float:
        """Berechnet den Median zweier sortierter Arrays in O(log(min(m, n))).

        Args:
            nums1: Erstes sortiertes Array
            nums2: Zweites sortiertes Array

        Returns:
            Median als Gleitkommazahl
        """
        # Stelle sicher, dass nums1 das kürzere Array ist
        if len(nums1) > len(nums2):
            nums1, nums2 = nums2, nums1

        m, n = len(nums1), len(nums2)
        left, right = 0, m
        half_len = (m + n + 1) // 2

        while left <= right:
            i1 = (left + right) // 2
            i2 = half_len - i1

            links1 = -float("inf") if i1 == 0 else nums1[i1 - 1]
            rechts1 = float("inf") if i1 == m else nums1[i1]
            links2 = -float("inf") if i2 == 0 else nums2[i2 - 1]
            rechts2 = float("inf") if i2 == n else nums2[i2]

            # Korrekte Trennlinie gefunden
            if links1 <= rechts2 and links2 <= rechts1:
                if (m + n) % 2 == 0:
                    return (max(links1, links2) + min(rechts1, rechts2)) / 2.0
                else:
                    return float(max(links1, links2))

            if links1 > rechts2:
                right = i1 - 1
            else:
                left = i1 + 1

        return 0.0
```

---

## Komplexitätsanalyse

| Dimension | Komplexität | Begründung |
| :--- | :--- | :--- |
| **[Zeitkomplexität](../glossary/o-notation.md)** | $\mathcal{O}(\log(\min(m, n)))$ | Die [[binäre Suche](../glossary/binary-search.md)](../glossary/binary-search.md) wird ausschließlich auf dem kürzeren Array der Länge $\min(m, n)$ ausgeführt. |
| **[Speicherkomplexität](../glossary/o-notation.md)** | $\mathcal{O}(1)$ | Es werden nur wenige Zeiger und Randvariablen verwendet. |

---

## Edge Cases & Fallstricke

- [x] **Ein Array ist komplett leer:** Die binäre Suche terminiert direkt mit dem Median des nicht-leeren Arrays.
- [x] **Ungleiche Längen:** Durch den anfänglichen Tausch `if len(nums1) > len(nums2)` ist garantiert, dass $i_2 \ge 0$ immer im gültigen Indexbereich von `nums2` liegt.
- [x] **Gerade vs. ungerade Gesamtlänge:** Bei ungerader Länge liefert $\max(\text{links}_1, \text{links}_2)$ exakt das Element in der Mitte; bei gerader Länge wird der Durchschnitt gebildet.
