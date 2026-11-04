---
tags:
  - LeetCode
  - Hash Table
  - String
  - Sliding Window
  - Medium
---



# LeetCode 3: Longest Substring Without Repeating Characters

- **Plattform:** [LeetCode #3](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
- **Schwierigkeit:** Medium
- **Kategorien:** Hash Table, String, [Sliding Window](../glossary/sliding-window.md)
- **Verwandte Konzepte:** [Schiebefenster (Sliding Window)](../glossary/sliding-window.md) | [Hash Map](../glossary/hash-map.md)

---

## Aufgabenstellung

Gegeben ist ein String `s`. Gesucht ist die Länge des **längsten zusammenhängenden Teilstrings** (*Substring*), der keine doppelten Zeichen enthält.

### Beispiele

```text
Input:  s = "abcabcbb"
Output: 3
Erklärung: Das längste Teilstück ohne Duplikat ist "abc" mit der Länge 3.

Input:  s = "bbbbb"
Output: 1
Erklärung: Das längste Teilstück ist "b" mit der Länge 1.

Input:  s = "pwwkew"
Output: 3
Erklärung: Das Teilstück "wke" hat die Länge 3 ("pwke" ist eine Subsequence, aber kein zusammenhängender Substring).
```

---

## Intuition & Lösungsansatz

### 1. Naive Idee (Brute Force)
Prüfe alle möglichen Teilstrings $s[i \dots j]$ ($0 \le i \le j < n$) darauf, ob alle Zeichen eindeutig sind.
- Laufzeit: $\mathcal{O}(n^3)$ bzw. $\mathcal{O}(n^2)$ mit Set.
- Flaschenhals: Bei $n = 5 \cdot 10^4$ viel zu langsam.

### 2. Optimierte Kernidee (Dynamisches Schiebefenster)
Wir spannen mit zwei Zeigern `start` und `end` ein dynamisches Fenster auf:
- Der Zeiger `end` wandert von links nach rechts durch den String.
- In einem Wörterbuch `seen` merken wir uns für jedes gesehene Zeichen dessen **zuletzt bekannten Index**: `seen[char] = end`.
- Taucht ein Zeichen auf, das bereits in `seen` vorhanden ist, setzen wir den linken Zeiger `start` direkt hinter das vorherige Vorkommen:
  $$\text{start} = \max(\text{start}, \text{seen}[\text{char}] + 1)$$
  *Wichtig:* Die $\max$-Funktion stellt sicher, dass sich `start` niemals nach links zurückbewegt, falls das gefundene Duplikat vor dem aktuellen Fensteranfang lag.
- Die Fensterlänge beträgt $\text{end} - \text{start} + 1$. Das Maximum über alle Schritte ist das gesuchte Ergebnis.

```mermaid
graph LR
    subgraph String "p w w k e w"
        W1["Index 1: 'w'"]
        W2["Index 2: 'w' (Kollision!)"]
    end
    W2 --> Jump["start springt direkt auf Index 2 (seen['w'] + 1)"]

    style W1 fill:#3f51b5,stroke:#fff,stroke-width:2px,color:#fff
    style W2 fill:#f44336,stroke:#fff,stroke-width:2px,color:#fff
    style Jump fill:#009688,stroke:#fff,stroke-width:2px,color:#fff
```

### 3. Wettbewerbs-Optimierung (0 ms Ansatz)
1. **ASCII-Array statt [Hash Map](../glossary/hash-map.md):** Da der String aus Standard-ASCII-Zeichen besteht, ist ein statisches Array `last = [-1] * 128` mit Index `ord(c)` schneller als Hash-Berechnungen.
2. **Vorzeitiger Abbruch:**
   - Sobald die aktuelle Maximallänge `best` der Anzahl aller unterschiedlichen Zeichen im Gesamtstring (`len(set(s))`) entspricht, kann kein längeres Fenster mehr existieren.
   - Wenn die noch verbleibende Restlänge $n - \text{start} \le \text{best}$ ist, wird die Schleife sofort abgebrochen.

---

## Implementierung (Python 3)

### Standard-Lösung (Sliding Window mit Hash Map)

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        """Ermittelt die Länge des längsten Teilstrings ohne doppelte Zeichen.

        Args:
            s: Eingabestring

        Returns:
            Maximale Länge eines teilstring-internen Fensters ohne Duplikate
        """
        seen = {}
        start = 0
        best = 0

        for end, char in enumerate(s):
            if char in seen:
                start = max(start, seen[char] + 1)

            seen[char] = end
            best = max(best, end - start + 1)

        return best
```

### High-Performance Variante (0 ms Benchmark)

```python
class SolutionFast:
    def lengthOfLongestSubstring(self, s: str) -> int:
        n = len(s)
        distinct = len(set(s))
        last = [-1] * 128
        start = best = 0

        for i, c in enumerate(s):
            code = ord(c)
            if last[code] >= start:
                start = last[code] + 1
                if best >= n - start:
                    break
            last[code] = i
            if i - start + 1 > best:
                best = i - start + 1
                if best == distinct:
                    break

        return best
```

---

## Komplexitätsanalyse

| Dimension | Komplexität | Begründung |
| :--- | :--- | :--- |
| **[Zeitkomplexität](../glossary/o-notation.md)** | $\mathcal{O}(n)$ | Der rechte Zeiger iteriert genau $n$-mal. Der Startzeiger springt ausschließlich vorwärts. |
| **[Speicherkomplexität](../glossary/o-notation.md)** | $\mathcal{O}(\min(n, |\Sigma|))$ | Die [Hash Map](../glossary/hash-map.md) speichert maximal so viele Einträge wie das Alphabet Zeichen hat ($|\Sigma| \le 128$ bei Standard-ASCII). |

---

## Edge Cases & Fallstricke

- [x] **Leerer String `""`:** Die Schleife läuft nicht durch, Rückgabewert ist korrekt $0$.
- [x] **String mit ausschließlich identischen Zeichen (z. B. `"bbbb"`):** `start` wandert bei jedem Schritt mit, Rückgabe ist $1$.
- [x] **Duplikat außerhalb des aktuellen Fensters (z. B. `"abba"`):** Beim zweiten `'a'` (Index 3) zeigt `seen['a'] = 0`. Ohne `max(start, ...)` würde der Startzeiger von $2$ fälschlicherweise auf $1$ zurückspringen.
