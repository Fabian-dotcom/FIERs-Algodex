---
tags:
  - Python
  - Performance
  - Optimization
  - Memory
  - Benchmark
---

# Python Performance-Optimierungen: Zero-Copy, String-Overhead & C-Speed

Micro-Optimierungen, die in Performance-kritischen Aufgaben (Zeitlimits auf großen Datenmengen) den Unterschied zwischen TLE und Accepted ausmachen — ohne den Algorithmus zu verändern.

---

## 1. Zero-Copy Indexing vs. Slicing

| Variante                                     | Speicherverhalten                              | Komplexität                      |
| :------------------------------------------- | :--------------------------------------------- | :------------------------------- |
| **Slicing** `arr[::2]`                       | Erzeugt eine **neue Liste** im Speicher        | $\mathcal{O}(n)$ Overhead        |
| **Index-Iteratoren** `range(0, len(arr), 2)` | Greifen direkt auf die Indizes zu, keine Kopie | $\mathcal{O}(1)$ Raumkomplexität |

```python
# Kopier-Overhead: baut eine zweite Liste
halbe = arr[::2]

# Zero-Copy: iteriert nur über Indizes
for i in range(0, len(arr), 2):
    x = arr[i]
```

Der Slicing-Allocator kann bei großen Arrays bzw. in engen Schleifen mehrfach GB-Einheiten allozieren; Index-Iteratoren bleiben vollständig kopierfrei ([verwandt: Generator-Ausdrücke](generator-expressions.md)).

---

## 2. Generator-Expressions in Aggregatfunktionen

Die Übergabe eines Generators (**ohne eckige Klammern** `[...]`) an `min()`, `max()`, `sum()` berechnet die Werte _on-the-fly_ (Lazy Evaluation) — die Liste wird **niemals als Ganzes** im Zwischenspeicher aufgebaut:

```python
total = sum(x * x for x in nums)      # O(1) Zusatzspeicher
total = sum([x * x for x in nums])    # O(n) Zusatzspeicher (Liste!)
```

Details und weitere Fallen: [Speicherschonende Generatoren](generator-expressions.md).

---

## 3. String-Allocation Overhead

String-Operationen (`str()`, Konkatenation, `int()`) sind auf großen Datenmengen **deutlich langsamer** als rein arithmetische Operationen, da sie Heap-Memory-Allokationen erfordern:

- Jede Konkatenation `a + b` alloziert ein neues String-Objekt.
- `int(s)`/`str(n)` kosten Parsing/Formatierung je Ziffer.
- **Regel:** Ziffernlogik (Modulo, Division, `bit_count()`) schlägt String-Umwege — siehe [Mathematische Zahlenumkehr](math-number-reversal.md).

Ein Paradebeispiel: Beim Vergleichen verschmolzener Zahlen ([Weekly 526 Q1](../solutions/leetcode-w526-q1.md)) sind String-Konkatenationen unvermeidbar — überall dort, wo es Alternativen gibt, ist die arithmetische Variante vorzuziehen.

---

## 4. Implizite Schleifenoptimierung (Built-in C-Speed)

Python-eigene Funktionen (`sum()`, `min()`, `max()`, `sorted()`) mit Generator-Ausdrücken laufen durch die Ausführung in **C extrem nah an der Hardware-Geschwindigkeit**, selbst wenn konzeptionell jedes Element einmal besucht werden muss ($\mathcal{O}(n)$):

```python
# C-Schleife: schneller als ein äquivalenter Python-for-Loop
best = max((f(x) for x in nums), default=0)
```

Zusätzlich lohnt bei Heap-Lastigem Code das **Lokal-Binden** der Hot-Path-Funktionen ([LeetCode 1851](../solutions/leetcode-1851.md)):

```python
heappush = heapq.heappush
heappop = heapq.heappop
```

Das eliminiert den Attribut-Lookup (`heapq.`) pro Aufruf in engen Sweeps.

---

## Wann einsetzen?

- **TLE trotz richtigem Algorithmus:** Erst diese vier Hebel prüfen, dann die Datenstruktur wechseln.
- **Speicherlimits:** Slicing → Index-Iterator, Listen-Comprehension → Generator.
- **Nicht überoptimieren:** Lesbarkeit schlägt Mikro-Gewinne, solange kein Limit betroffen ist.
