---
tags:
  - Python
  - Optimization
  - Generator
  - Memory Management
  - Performance
---

# Speicherschonende Generator-Ausdrücke (O(1) Space)

In Python entscheidet die Wahl zwischen einer **List Comprehension** (`[...]`) und einem **Generator-Ausdruck** (`(...)`) oft darüber, ob ein Algorithmus bei großen Eingaben mit $\mathcal{O}(1)$ Zusatzspeicher auskommt oder wegen $\mathcal{O}(n)$ Speicherallokation in ein *Memory Limit Exceeded (MLE)* läuft.

---

## 1. List Comprehension vs. Generator Expression

### List Comprehension (`[...]`) – Eager Evaluation
```python
# Erzeugt eine vollständige neue Liste im RAM, BEVOR sum() beginnt:
ans = sum([x * 2 for x in nums])
```
- **Ablauf:** Allokiert Speicher für $n$ Ganzzahlen auf dem Heap.
- **Speicheraufwand:** $\mathcal{O}(n)$ Bytes. Bei $n = 10^7$ belegt dies hunderte Megabytes Arbeitsspeicher!
- **Garbage Collection:** Nach der Berechnung muss die temporäre Liste vom Garbage Collector wieder abgeräumt werden.

### Generator Expression (`(...)`) – Lazy Evaluation
```python
# Verarbeitet Elemente "on the fly" ohne temporäre Liste:
ans = sum(x * 2 for x in nums)
```
- **Ablauf:** Der Generator erzeugt immer nur **ein einziges Element auf Abruf** (*yield*), übergibt es direkt an den Akkumulator von `sum()` und verwirft es sofort wieder.
- **Speicheraufwand:** $\mathcal{O}(1)$ konstanter Speicherbedarf, unabhängig davon, ob $n = 10$ oder $n = 10^9$ ist!

```mermaid
graph TD
    subgraph List Comprehension [O(n) Space]
        LC1["Array im RAM: [elem_1, elem_2, ..., elem_n]"] --> LC2["sum() iteriert ueber Liste"]
    end

    subgraph Generator Expression [O(1) Space]
        GE1["Element erzeugen"] -->|yield| GE2["Akkumulator addiert"]
        GE2 -->|verwerfen| GE1
    end

    style LC1 fill:#f44336,stroke:#fff,stroke-width:2px,color:#fff
    style GE2 fill:#4caf50,stroke:#fff,stroke-width:2px,color:#fff
```

---

## 2. Best Practices & Stolpersteine

### 1. Klammern weglassen bei Funktionsaufrufen
Wird ein Generator-Ausdruck als einziges Argument an eine Funktion wie `sum()`, `min()`, `max()`, `any()` oder `all()` übergeben, sind keine doppelten Klammern nötig:

```python
# Richtig und speichereffizient:
has_even = any(x % 2 == 0 for x in nums)
max_length = max(len(word) for word in words)

# Unnoetiger Speicherverbrauch:
has_even = any([x % 2 == 0 for x in nums])  # Allokiert unnoetig Boolean-Liste!
```

### 2. Kurzschlussauswertung (Short-Circuiting) bei `any()` und `all()`
Bei Generatoren bricht Python sofort ab, sobald das Ergebnis feststeht:
```python
# Bricht nach dem ERSTEN geraden Element sofort ab:
is_valid = any(expensive_check(x) for x in nums)

# Führt expensive_check() fuer ALLE Elemente aus, bevor any() prueft:
is_valid = any([expensive_check(x) for x in nums])
```

---

## 3. Vergleichstabelle

| Kriterium | List Comprehension `[...]` | Generator Expression `(...)` |
| :--- | :--- | :--- |
| **Auswertungsstrategie** | Eager (sofort, vollständig) | Lazy (bei Bedarf, Element für Element) |
| **Speicherkomplexität** | $\mathcal{O}(n)$ | $\mathcal{O}(1)$ |
| **Geeignet für** | Wenn das Ergebnis mehrfach indiziert werden muss (`list[i]`) | Reine Reduktionen (`sum`, `min`, `max`, `all`, `any`) |
| **Short-Circuiting** | Nein (berechnet immer alle $n$ Elemente) | Ja (sofortiger Abbruch bei Abbruchbedingung) |
| **GC-Overhead** | Hoch (Heap-Allokation und Deallokation) | Minimal (kein Zwischen-Array) |
