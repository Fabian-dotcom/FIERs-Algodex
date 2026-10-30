---
tags:
  - Math
  - Array
  - Permutation
  - Cyclic Shift
---



# Zyklische Permutationen & Rotationen

Eine **Permutation** der Zahlen $0, 1, \dots, n-1$ ist eine Anordnung, in der jedes Element aus $\{0, 1, \dots, n-1\}$ genau einmal vorkommt.

---

## 1. Zyklische Rotationen prüfen

Häufig muss geprüft werden, ob ein Array eine verschobene (zyklisch rotierte) Version der sortierten Sequenz ist.

Befindet sich die Zahl $0$ an Index $z = \text{nums.index}(0)$, muss für eine **aufsteigende Rotation** gelten:
$$\text{nums}[(z + i) \pmod n] = i \quad \text{für alle } i \in \{0, \dots, n-1\}$$

Für eine **absteigend sortierte Rotation** (gespiegelte Sequenz) gilt:
$$\text{nums}[(z - i) \pmod n] = i \quad \text{für alle } i \in \{0, \dots, n-1\}$$

```python
# Schneller Invarianz-Check in Python:
is_increasing = all(nums[(zero_pos + i) % n] == i for i in range(n))
is_decreasing = all(nums[(zero_pos - i) % n] == i for i in range(n))
```

---

## 2. Minimale Operationen zur Sortierung

Darf ein Array nur durch **zyklische Linksshifts** und **vollständige Umkehrungen (Reverse)** sortiert werden (wie in [LeetCode 3942](../solutions/leetcode-3942.md)):

1. Ist das Array bereits sortiert $\to 0$ Operationen.
2. Ist es eine **aufsteigende Rotation**:
   - Nur Links-Rotationen: $z$ Züge.
   - Umkehren, Rotieren, Umkehren: $n - z + 2$ Züge.
   - Minimale Kosten: $\min(z, n - z + 2)$.
3. Ist es eine **absteigende Rotation**:
   - Steht die 0 an Index 0: 1 Zug (einmal umkehren genügt).
   - Andernfalls: $\min(z + 2, n - z)$ Züge.
4. Trifft keines von beidem zu, ist eine Sortierung allein über diese beiden Operationen unmöglich (Rückgabe: $-1$).

---

## Komplexität

- **[Zeitkomplexität](o-notation.md):** $\mathcal{O}(n)$ – Das Finden der $0$ und die Validierung der Invariante erfolgen in linearen Durchläufen.
- **[Speicherkomplexität](o-notation.md):** $\mathcal{O}(1)$.
