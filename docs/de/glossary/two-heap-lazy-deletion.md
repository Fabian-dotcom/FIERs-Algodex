---
tags:
  - Data Structure
  - Heap
  - Priority Queue
  - Median
  - Lazy Deletion
  - Sliding Window
---

# Two-Heap mit Lazy Deletion & Median-Kosten (L1-Norm)

Das **Two-Heap-Pattern** hält die untere und obere Hälfte eines gleitenden Fensters in zwei balancierten Heaps und liefert Median sowie die Summe der absoluten Abstände ($L_1$-Norm) in amortisiert $\mathcal{O}(\log x)$ pro Schritt.

---

## Wann einsetzen?

- Der **Median** eines gleitenden Fensters der Größe $x$ muss nach jedem Schritt aktuell gehalten werden.
- Zusätzlich wird die **Summe der absoluten Abstände** zum Median benötigt:
  $$\sum_{i} |a_i - \text{median}|$$
  (das klassische _Minimum Cost to Make Array K-Special / Equal_-Kriterium, z. B. [LeetCode 3841](../solutions/leetcode-3841.md)).
- Eine naive Sortierung pro Fenster würde $\mathcal{O}(n \cdot x \log x)$ kosten — der Two-Heap-Ansatz schafft $\mathcal{O}(n \log x)$.

---

## Kernmechanik

### Zwei balancierte Heaps

| Heap    | Richtung                | Inhalt        | Invariante                                        |
| :------ | :---------------------- | :------------ | :------------------------------------------------ |
| `small` | Max-Heap (via Negation) | untere Hälfte | $\text{len}(small) = \text{len}(large)$ oder $+1$ |
| `large` | Min-Heap                | obere Hälfte  | alle Elemente $\ge$ alle Elemente in `small`      |

- **Gerade Fenstergröße:** Median $= \frac{small[0] + large[0]}{2}$
- **Ungerade Fenstergröße:** Median $= small[0]$ (kleinere Hälfte hält das Extra-Element)

### Lazy Deletion

Elemente, die das Fenster verlassen, werden **nicht** teuer aus dem Heap gesucht (`O(n)`-Suche), sondern nur in einer Häufigkeits-Tabelle `invalid` markiert:

```python
invalid[verlassenes_element] += 1   # O(1) markieren
```

Erst wenn ein solches Element **wirklich an die Spitze** eines Heaps wandert, wird es dort aufgeräumt:

```python
while invalid[small[0]]:
    invalid[small[0]] -= 1
    heapq.heappop(small)
```

Das spart die lineare Suche und amortisiert die Aufräumkosten über alle zukünftigen Pops.

### Median-Kosten in $\mathcal{O}(1)$ pro Abfrage

Beide Heaps führen laufende **Summen** (`small_sum`, `large_sum`) mit:

```python
cost = median * len(small) - small_sum + large_sum - median * len(large)
```

Damit ist die $L_1$-Kostenabfrage konstant, nur die Fensterpflege kostet $\mathcal{O}(\log x)$.

---

## Python-Skelett

```python
import heapq
from collections import defaultdict

small, large = [], []          # Max-Heap (negiert), Min-Heap
small_sum = large_sum = 0
invalid = defaultdict(int)
small_size = large_size = 0    # effektive (nicht-lazy) Größen

def prune(heap: list, is_small: bool) -> None:
    """Markierte Elemente an der Spitze physisch entfernen."""
    sign = -1 if is_small else 1
    while heap and invalid[sign * heap[0]]:
        invalid[sign * heap[0]] -= 1
        heapq.heappop(heap)

def rebalance() -> None:
    """Invariante len(small) == len(large) bzw. len(small) == len(large)+1."""
    global small_size, large_size
    prune(small, True); prune(large, False)
    if small_size > large_size + 1:
        val = -heapq.heappop(small); small_sum -= val; small_size -= 1
        heapq.heappush(large, val); large_sum += val; large_size += 1
    elif small_size < large_size:
        val = heapq.heappop(large); large_sum -= val; large_size -= 1
        heapq.heappush(small, -val); small_sum += val; small_size += 1
```

---

## Komplexität

| Operation                    | Komplexität                  | Begründung                                                   |
| :--------------------------- | :--------------------------- | :----------------------------------------------------------- |
| **Element hinzufügen**       | $\mathcal{O}(\log x)$        | Push + Rebalance.                                            |
| **Element entfernen (lazy)** | $\mathcal{O}(1)$ amortisiert | Nur Markierung; Aufräumen verteilt sich auf zukünftige Pops. |
| **Median abfragen**          | $\mathcal{O}(1)$             | Spitze des gewichteten Heaps.                                |
| **$L_1$-Kosten abfragen**    | $\mathcal{O}(1)$             | Geschlossene Formel aus den mitgeführten Summen.             |
| **Speicherplatz**            | $\mathcal{O}(x)$             | Zwei Heaps + Häufigkeits-Tabelle.                            |
