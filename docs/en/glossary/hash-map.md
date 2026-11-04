---
tags:
  - Data Structure
  - Hash Table
  - Array
---



# Hash Map & Hash Set

Eine **Hash Map** (in Python `dict`) und ein **Hash Set** (`set`) gehören zu den grundlegendsten und mächtigsten Datenstrukturen in der Softwareentwicklung und bei algorithmischen Aufgaben. Sie ermöglichen den Zugriff auf Werte über Schlüssel im durchschnittlichen Zeitaufwand von $\mathcal{O}(1)$.

---

## Intuition & Kernidee

Statt ein Array der Länge $n$ sequenziell zu durchsuchen ($\mathcal{O}(n)$), transformiert eine **Hash-Funktion** einen beliebigen Schlüssel (Zahl, String, Tupel) deterministisch in einen ganzzahligen Index eines internen Speicher-Arrays (*Buckets*).

- **Lookup / Einfügen / Löschen:** Findet im Idealfall über direkte Speicheradressierung in $\mathcal{O}(1)$ statt.
- **Kollisionen:** Haben zwei unterschiedliche Schlüssel denselben Hash-Wert, werden Kollisionsauflösungsverfahren wie Chaining (Verkettung) oder Open Addressing (offene Adressierung) eingesetzt.

```mermaid
graph LR
    Key["Schlüssel: 'target'"] --> Hash["Hash-Funktion: hash(key)"]
    Hash --> Index["Index: 4"]
    Index --> Bucket["Bucket-Array[4]: Wert"]

    style Key fill:#3f51b5,stroke:#fff,stroke-width:2px,color:#fff
    style Hash fill:#009688,stroke:#fff,stroke-width:2px,color:#fff
    style Bucket fill:#ff9800,stroke:#fff,stroke-width:2px,color:#fff
```

---

## Typische Einsatzmuster in LeetCode

### 1. Das Komplement-Muster (Two Sum)
Beim Durchlaufen eines Arrays wird für das aktuelle Element $x$ geprüft, ob das gesuchte Gegenstück $\text{target} - x$ bereits in der Hash Map existiert. Ist dies der Fall, hat man das Paar in einem einzigen Durchlauf gefunden ($\mathcal{O}(n)$ statt $\mathcal{O}(n^2)$).

```python
seen = {}
for i, num in enumerate(nums):
    complement = target - num
    if complement in seen:
        return [seen[complement], i]
    seen[num] = i
```

### 2. Zuletzt gesehene Indizes (Sliding Window / Intervalle)
In Zeichenketten- und Teilarray-Aufgaben speichert die Hash Map das letzte Vorkommen eines Elements `seen[char] = index`. Taucht ein Duplikat auf, kann das linke Fensterende direkt hinter die vorherige Position springen.

### 3. Frequenzzähler (Frequency Counting)
Zählen von Vorkommen bestimmter Zustände, [Bitmasken](bit-manipulation.md) oder Elemente. In Python steht dafür `collections.Counter` oder `collections.defaultdict(int)` zur Verfügung.

---

## Komplexität

| Operation | Durchschnittlich | Worst-Case (viele Kollisionen) |
| :--- | :--- | :--- |
| **Lookup (`key in dict`)** | $\mathcal{O}(1)$ | $\mathcal{O}(n)$ |
| **Insert (`dict[key] = val`)** | $\mathcal{O}(1)$ | $\mathcal{O}(n)$ |
| **Delete (`del dict[key]`)** | $\mathcal{O}(1)$ | $\mathcal{O}(n)$ |
| **Speicherplatz** | $\mathcal{O}(n)$ | $\mathcal{O}(n)$ |

---

## Stolpersteine & Details

1. **Unveränderliche Schlüssel:** Nur unhashbare Datentypen (z. B. Listen oder Sets) werfen einen `TypeError: unhashable type`. In Python müssen Schlüssel unveränderlich (*immutable*) sein (z. B. `tuple`, `str`, `int`, `frozenset`).
2. **Speicher-Overhead:** Hash Maps reservieren mehr Speicherplatz als reine Arrays, um Kollisionen gering zu halten. Bei strikt begrenzten Werten (z. B. reine ASCII-Zeichen) ist ein statisches Array `[0] * 128` oft deutlich schneller und speichereffizienter.
3. **Worst-Case-Laufzeit:** Im Worst-Case (z. B. Denial-of-Service durch absichtlich erzeugte Kollisionen) kann ein Hash-Lookup auf $\mathcal{O}(n)$ degradieren. In Python verwendet die Standardbibliothek SipHash, um solchen Angriffen vorzubeugen.
