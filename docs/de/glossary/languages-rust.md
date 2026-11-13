---
tags:
  - Rust
  - Python
  - Languages
  - Learning
---

# Sprachen & Migration (Python → Rust)

Dieser Bereich ist das Zuhause aller **sprachspezifischen** Dokumentation. Der Algodex ist historisch in Python aufgebaut (`python`/`python3`-Codeblöcke); hier lernen wir, dieselben Algorithmen in **Rust** zu lesen, zu schreiben und die Spracheigenschaften gegeneinander abzuwägen.

---

## Warum Rust für Algorithmen?

| Aspekt               | Python                                     | Rust                                                                                                       |
| :------------------- | :----------------------------------------- | :--------------------------------------------------------------------------------------------------------- |
| **Typsystem**        | Dynamisch, Type Hints optional             | Statisch, zur Kompilierzeit geprüft                                                                        |
| **Integer-Overflow** | Unbegrenzte Big-Ints automatisch           | Feste Bitbreiten (`i32`, `i64`, `u64`, …) – Summen bewusst wählen                                          |
| **Speichermodell**   | Garbage Collector, Heap-Objekte            | Ownership & Borrow Checker, deterministisch zur Compile-Zeit (siehe [Speicher & GC](memory-management.md)) |
| **Geschwindigkeit**  | Interpreter, C-Built-ins als Beschleuniger | Native Maschinencode, konkurriert mit C/C++                                                                |
| **Collections**      | `list`, `dict`, `collections.deque`        | `Vec`, `HashMap`, `VecDeque`                                                                               |
| **Einstieg**         | Eine Zeile Script                          | `cargo new`, Typ-Annotationen, Borrowing-Regeln                                                            |

---

## Python ↔ Rust Übersetzungstabelle

| Python                                           | Rust                                                                | Bemerkung                                          |
| :----------------------------------------------- | :------------------------------------------------------------------ | :------------------------------------------------- |
| `arr = [0] * n`                                  | `let arr = vec![0; n];`                                             | Vorallokation, kein Re-Alloc                       |
| `for i, x in enumerate(arr):`                    | `for (i, &x) in arr.iter().enumerate()`                             | `&x` entpackt die Referenz                         |
| `for i in reversed(range(n))`                    | `for i in (0..n).rev()`                                             | Ranges statt Index-Funktionen                      |
| `list.append(x)` / `list.pop()`                  | `vec.push(x)` / `vec.pop()`                                         |                                                    |
| `collections.deque` (`append`, `pop`, `popleft`) | `std::collections::VecDeque` (`push_back`, `pop_back`, `pop_front`) | $\mathcal{O}(1)$ an beiden Enden                   |
| `heapq` (`heappush`, `heappop`)                  | `std::collections::BinaryHeap` (Max-Heap; Min über `Reverse`)       | Rust std hat keinen Min-Heap direkt                |
| `d = {}` / `d[k] = v`                            | `let mut d = HashMap::new();` / `d.insert(k, v);`                   | Zugriff via `d.get(&k)` liefert `Option<&V>`       |
| `sorted(arr)`                                    | `arr.sort()` (in-place) oder `arr.to_vec().sort()`                  | `sort_unstable()` ist schneller, aber nicht stabil |
| `arr[-1]`                                        | `*arr.last().unwrap()` oder `arr[arr.len() - 1]`                    | Negative Indizes gibt es nicht                     |
| `a, b = b, a + b`                                | `let tmp = a; a = b; b = tmp;` oder `(a, b) = (b, a + b);`          | Tuple-Swap seit Rust 1.59                          |
| `max(x, default=0)`                              | `x.max(0)`                                                          | Methoden statt Built-ins                           |
| `float("inf")`                                   | `i64::MAX` / `f64::INFINITY`                                        | Typabhängig                                        |
| `if x not in seen:`                              | `if !seen.contains(&x)` (Set)                                       | `&` bei Borrow-Typen nötig                         |
| `f-strings f"{x}"`                               | `format!("{x}")`                                                    | Gleiche `{}`-Syntax                                |
| `class Node:`                                    | `struct Node { ... }`                                               | Structs statt Klassen; Verhalten über `impl`       |
| `None`                                           | `Option<T>` (`None` / `Some(t)`)                                    | Kein `null` – der Compiler zwingt zur Behandlung   |
| Exceptions (`raise`)                             | `Result<T, E>` (`Err` / `?`-Operator)                               | Fehler sind Werte, keine Stack-Unwinds             |

---

## Rust-Konzepte, die man am Anfang immer wieder stolpert

1. **Ownership & Borrowing:** Jeder Wert hat genau einen Besitzer. `&x` liest (beliebig viele), `&mut x` schreibt (nur einer gleichzeitig). Die DSU-Implementierung ([Union-Find](dsu-union-find.md)) zeigt, warum `find` `&mut self` braucht: Path Compression schreibt.
2. **`Option` statt `None`-Checks:** `stack.back().copied().unwrap_or(j)` ist das Rust-Idiom für `stack[-1] if stack else j` (siehe [Monotonic Stack](monotonic-stack-cost-accumulation.md)).
3. **Integer-Typen bewusst wählen:** `usize` für Indizes/Lengths, `i64` für Summen. Bei $n \cdot \max(\text{val})$ über $10^{18}$ → `i128`.
4. **`while let Some(x) = ...`:** Rusts idiomatisches Muster für „solange es etwas gibt“ – entspricht Pythons `while stack:`.
5. **Iteratoren statt Schleifen-Index:** `(0..n).map(...).sum()` kompiliert oft auf die gleiche Maschinenschleife wie die handgeschriebene `for`-Version – Iteratoren sind **nicht** langsamer.

---

## Lern-Roadmap Rust (empfohlener Weg)

1. **Syntax & Control Flow:** Variablen (`let mut`), Funktionen, `match` statt `switch`.
2. **Collections:** `Vec`, `VecDeque`, `HashMap`, `String` vs `&str`.
3. **Ownership-Basics:** Move-Semantik, Referenzen, Lifetime-Intuition (noch ohne explizite Lifetimes).
4. **Erste Algorithmen portieren:** Die einfachen Glossar-Muster zuerst (z. B. [Sliding Window](sliding-window.md)), dann [DSU](dsu-union-find.md) mit `&mut self`.
5. **Traits & Generics:** `impl`, `derive(Debug)`, eigene Traits für Heap-Vergleiche (`Ord`).
6. **Result & Fehlerbehandlung:** LeetCode-artige Signaturen `fn f(...) -> Result<i64, String>` im Blick behalten.

---

## Strategie im Algodex

Jedes **neue** Glossar-Kapitel dokumentiert von nun an die Referenz in **beiden** Sprachen: Python zuerst (Historie, schnelle Iteration) und die Rust-Variante mit den sprachspezifischen Fallstricken als eigene Untersektion _„Rust-Notizen“_. Bestehende Kapitel werden nach und nach erweitert – angefangen bei [Sliding Window](sliding-window.md), [Monotonic Stack with Cost Accumulation](monotonic-stack-cost-accumulation.md) und [DSU / Union-Find](dsu-union-find.md).
