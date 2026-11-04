---
tags:
  - Math
  - String
  - Greedy
---



# Römische Zahlen & Ziffernsysteme

Das römische Zahlensystem ist ein additives und subtraktives Zahlensystem. Es verwendet sieben Grundsymbole:

| Symbol | Wert |
| :---: | :---: |
| **I** | 1 |
| **V** | 5 |
| **X** | 10 |
| **L** | 50 |
| **C** | 100 |
| **D** | 500 |
| **M** | 1000 |

---

## Regeln des Systems

1. **Additive Regel:** Symbole werden von links nach rechts addiert, wenn ein Symbol größer oder gleich seinem Nachfolger ist (z. B. $\text{VI} = 5 + 1 = 6$, $\text{XV} = 10 + 5 = 15$).
2. **Subtraktive Regel:** Steht ein kleineres Symbol unmittelbar vor einem größeren, wird sein Wert subtrahiert (z. B. $\text{IV} = 4$, $\text{IX} = 9$, $\text{XL} = 40$, $\text{XC} = 90$, $\text{CD} = 400$, $\text{CM} = 900$).

---

## Konvertierungsstrategien

### 1. Integer zu Roman (Greedy-Ansatz)
Da die Symbole in strikt absteigender Wertigkeit angeordnet sind, lässt sich jede Zahl gierig (*greedy*) von oben nach unten zerlegen. Man definiert eine Wertetabelle, die sowohl die Grundsymbole als auch die 6 subtraktiven Ausnahmefälle enthält:

```python
VAL_MAP = [
    (1000, "M"),
    (900, "CM"),
    (500, "D"),
    (400, "CD"),
    (100, "C"),
    (90, "XC"),
    (50, "L"),
    (40, "XL"),
    (10, "X"),
    (9, "IX"),
    (5, "V"),
    (4, "IV"),
    (1, "I"),
]

result = []
for val, sym in VAL_MAP:
    while num >= val:
        result.append(sym)
        num -= val
return "".join(result)
```

**Alternative:** Direkte Zerlegung nach Stellenwerten (Tausender, Hunderter, Zehner, Einer) über Tupel-Lookups in $\mathcal{O}(1)$.

### 2. Roman zu Integer (Rückwärts-Traversierung)
Beim Lesen eines römischen Strings von rechts nach links ist die Logik besonders elegant:
- Merke den Wert des vorigen (rechten) Zeichens `prev_val`.
- Ist das aktuelle Zeichen kleiner als `prev_val`, liegt ein subtraktiver Fall vor $\rightarrow \text{total} -= \text{val}$.
- Ist es größer oder gleich, wird es regulär addiert $\rightarrow \text{total} += \text{val}$.

```python
roman_map = {"I": 1, "V": 5, "X": 10, "L": 50, "C": 100, "D": 500, "M": 1000}
total = 0
prev_val = 0

for char in reversed(s):
    val = roman_map[char]
    if val < prev_val:
        total -= val
    else:
        total += val
    prev_val = val
return total
```

---

## Komplexität

| Operation | [Zeitkomplexität](o-notation.md) | [Speicherkomplexität](o-notation.md) |
| :--- | :--- | :--- |
| **Integer to Roman** | $\mathcal{O}(1)$ (da Wertebereich $1 \le \text{num} \le 3999$) | $\mathcal{O}(1)$ |
| **Roman to Integer** | $\mathcal{O}(n)$ mit $n \le 15$ $\rightarrow \mathcal{O}(1)$ | $\mathcal{O}(1)$ |
