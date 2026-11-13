---
tags:
  - LeetCode
  - Array
  - Math
  - Number Theory
  - Greedy
  - Medium
---

# LeetCode Weekly 526 Q2: Minimize the Maximum Value of GCD-Connected Array

- **Plattform:** Weekly Contest 526, Q2
- **Schwierigkeit:** Medium
- **Kategorien:** Array, Math, Number Theory, Greedy
- **Verwandte Konzepte:** [Bitweise Operationen](../glossary/bit-manipulation.md) | [Ein-Pass durch algebraische Umformung](../glossary/algebraic-one-pass.md)

---

## Aufgabenstellung

Ein Array `nums` der Länge $n$ heißt **GCD-Connected**, wenn:

- $\text{nums}[i] > 0$ für alle $i$,
- strikt aufsteigend: $\text{nums}[i] < \text{nums}[i+1]$,
- $\text{nums}[\text{index}] = \text{value}$ fixiert ist,
- $\gcd(\text{nums}[i], \text{nums}[i+1]) > 1$ für alle benachbarten Paare.

Gib das **minimale mögliche Maximum** $\text{nums}[n-1]$ zurück, oder $-1$, falls kein solches Array existiert.

### Beispiele

```text
Input:  n = 4, index = 2, value = 8
Output: 14
Erklärung: z. B. [4, 6, 8, 10] — alle Nachbarn teilen einen gemeinsamen Faktor ≥ 2.
```

---

## Intuition & Lösungsansatz

### Optimierte Kernidee (Kleinster-Primfaktor-Kette)

1. **Benachbarte Werte unterscheiden sich um mindestens 2**, denn $\gcd(x, x+1) = 1$ — aufeinanderfolgende Zahlen sind immer teilerfremd.
2. **Für $y > x$ mit $\gcd(x, y) = g > 1$** gilt $g \mid (y - x)$, also ist der **kleinste erreichbare Abstand** $y - x \ge \text{spf}(x)$ (kleinster Primfaktor von $x$). Die minimal wachsende Kette läuft daher in Zweierschritten ab dem kleinsten Primfaktor.
3. **Rechts von `index`:** Ist `value` gerade ($p = 2$), folgt `value + 2m` für $m = n - 1 - \text{index}$ weitere Elemente. Ist `value` ungerade mit kleinstem Primfaktor $p$, springt man zuerst auf das gerade `value + p` und dann in Zweierschritten: $\text{value} + p + 2(m-1)$.
4. **Links von `index`:** Die maximale Elementzahl inklusive `value` beträgt `value / 2` (gerades `value`) bzw. $1 + (value - p)/2$ (ungerades). Übersteigt `index + 1` dieses Budget, gibt es kein gültiges Array → $-1$.

Die Trail-and-Error-Suche nach der Kettenlänge entfällt komplett — die Antwort ist eine **geschlossene Formel** plus $\mathcal{O}(\sqrt{\text{value}})$-Probedivision für den kleinsten Primfaktor.

---

## Implementierung (Python 3)

```python
class Solution:
    def minMax(self, n: int, index: int, value: int) -> int:
        """Bestimmt das minimale Maximum eines GCD-Connected-Arrays.

        Args:
            n: Länge des Zielarrays
            index: Fixierte Position
            value: Fixierter Wert an position index

        Returns:
            Minimales mögliches nums[n-1], oder -1
        """
        if n == 1:
            return value
        if value == 1:
            return -1  # gcd mit 1 ist nie > 1

        # Kleinster Primfaktor von value bestimmen
        if value & 1 == 0:
            p = 2
        else:
            p = value
            d = 3
            while d * d <= value:
                if value % d == 0:
                    p = d
                    break
                d += 2

        # Maximale Elementzahl links inkl. value:
        # gerade -> 2, 4, ..., value (value/2 Elemente)
        # ungerade -> value - p ist gerade, dann Zweierschritte abwärts
        left = value >> 1 if p == 2 else 1 + ((value - p) >> 1)
        if index + 1 > left:
            return -1

        m = n - 1 - index   # Anzahl Elemente rechts von value
        if m == 0:
            return value
        if p == 2:
            return value + 2 * m
        return value + p + 2 * (m - 1)
```

---

## Komplexitätsanalyse

| Dimension                                            | Komplexität                        | Begründung                                                                          |
| :--------------------------------------------------- | :--------------------------------- | :---------------------------------------------------------------------------------- |
| **[Zeitkomplexität](../glossary/o-notation.md)**     | $\mathcal{O}(\sqrt{\text{value}})$ | Probedivision für den kleinsten Primfaktor; der Rest sind $\mathcal{O}(1)$-Formeln. |
| **[Speicherkomplexität](../glossary/o-notation.md)** | $\mathcal{O}(1)$                   | Nur Skalare.                                                                        |

---

## Edge Cases & Fallstricke

- [x] **`value == 1`:** $\gcd(1, x) = 1$ immer → kein gültiges Array.
- [x] **$n = 1$:** Das Array besteht nur aus `value` selbst, alle Bedingungen trivial erfüllt.
- [x] **Ungerades `value`:** Der erste Nachbarn rechts ist `value + p` (ungerade Vielfachheit des Primfaktors), danach Zweierschritte — nicht blind `+2`.
- [x] **Linksbudget:** Werden mehr Positionen links von `index` benötigt als konstruierbar, ist $-1$ die Antwort.
