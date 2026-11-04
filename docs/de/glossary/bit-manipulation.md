---
tags:
  - Bit Manipulation
  - Math
  - Permutation
---



# Bitweise Operationen & Bitmasken

Bitweise Operationen verarbeiten Zahlen direkt auf ihrer binären Repräsentation. Sie sind extrem schnell (wenige CPU-Zyklen) und erlauben es, Mengen, Zustände und Paritäten kompakt abzubilden.

---

## Die Kernoperatoren

| Operator | Name | Bedeutung | Typischer Zweck |
| :---: | :---: | :---: | :---: |
| `&` | AND | Beide Bits müssen 1 sein | Maskierung, Schnittmenge |
| `\|` | OR | Mindestens ein Bit ist 1 | Vereinigung, Bit setzen |
| `^` | XOR | Genau ein Bit ist 1 | Parität, Differenz, Bit toggeln |
| `~` | NOT | Invertiert alle Bits | Einerkomplement |
| `<<` | Shift Links | Multiplikation mit $2^k$ | Bit an Position $k$ schieben |
| `>>` | Shift Rechts | Ganzzahl-Division durch $2^k$ | Bits nach rechts schieben |

---

## Wichtige Bit-Tricks

### 1. Paritätsprüfung & Palindrom-Bedingung
Soll geprüft werden, ob eine Zahl höchstens ein einziges gesetztes Bit besitzt (eine Zweierpotenz oder 0):
$$\text{mask} \ \& \ (\text{mask} - 1) == 0$$

- Wenn genau ein Bit gesetzt ist: $\text{mask} - 1$ kippt das niederwertigste 1-Bit zu 0 und alle nachfolgenden 0-Bits zu 1. Das bitweise AND ergibt exakt 0.
- Dies ist das Herzstück aller Pfad-Palindrom-Prüfungen (z. B. in [LeetCode 2791](../solutions/leetcode-2791.md) und [LeetCode 3841](../solutions/leetcode-3841.md)).

### 2. Akkumulierendes Bitweises AND
Ist für ein Permutations- oder Sortierproblem gefordert, dass zwei Elemente an Position $i$ und $j$ nur getauscht werden dürfen, wenn für ein $k$ gilt: $\text{nums}[i] \ \& \ k == k$ und $\text{nums}[j] \ \& \ k == k$ (wie in [LeetCode 3644](../solutions/leetcode-3644.md)):

Damit ein Element $x$ mit seiner Zielposition $i$ interagieren kann, muss $k$ eine Teilmenge der Bits aller fehlsortierten Elemente sein:
$$k_{\max} = \bigwedge_{i: \text{nums}[i] \neq i} \text{nums}[i]$$

Ist das Array bereits sortiert, gibt es keine Restriktionen (Ergebnis: 0).

### 3. Niederwertigstes gesetztes Bit (Lowest Set Bit)
$$x \ \& \ (-x)$$
Dieser Ausdruck isoliert das niedrigstwertige gesetzte 1-Bit von $x$ (die Basis von Fenwick-Bäumen).
