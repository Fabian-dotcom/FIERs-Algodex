---
tags:
  - LeetCode
  - Math
  - String
  - Hash Table
  - Easy
---



# LeetCode 13: Roman to Integer

- **Plattform:** [LeetCode #13](https://leetcode.com/problems/roman-to-integer/)
- **Schwierigkeit:** Easy
- **Kategorien:** Math, String, Hash Table
- **Verwandte Konzepte:** [Römische Zahlen & Ziffernsysteme](../glossary/roman-numerals.md)

---

## Aufgabenstellung

Gegeben ist eine gültige [römische Zahl](../glossary/roman-numerals.md) als String `s`. Konvertiere sie in eine Ganzzahl.

### Römische Symbole & Werte

| Symbol | I | V | X | L | C | D | M |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Wert** | 1 | 5 | 10 | 50 | 100 | 500 | 1000 |

### Beispiele

```text
Input:  s = "III"
Output: 3

Input:  s = "LVIII"
Output: 58
Erklärung: L = 50, V = 5, III = 3

Input:  s = "MCMXCIV"
Output: 1994
Erklärung: M = 1000, CM = 900, XC = 90, IV = 4
```

---

## Intuition & Lösungsansatz

### 1. Naive Idee (Vorwärts-Lookup mit 2-Zeichen-Fenster)
Man läuft von links nach rechts und prüft für jedes Zeichenpaar, ob es ein Spezialfall wie `"IV"` oder `"IX"` ist.
- Nachteil: Erfordert Grenzprüfungen (`i + 1 < len(s)`), um Index-Fehler zu vermeiden.

### 2. Optimierte Kernidee (Rückwärts-Traversierung)
Wenn man die [[römische Zahl](../glossary/roman-numerals.md)](../glossary/roman-numerals.md) **von rechts nach links** (rückwärts) liest, wird die Regel extrem einfach:
- Wir merken uns den Wert des zuletzt verarbeiteten (rechten) Zeichens `prev_val`.
- Ist der Wert des aktuellen Zeichens **kleiner** als `prev_val`, liegt eine Subtraktion vor (z. B. I vor V $\to 5 - 1 = 4$). Wir subtrahieren den Wert von der Gesamtsumme.
- Ist der Wert des aktuellen Zeichens **größer oder gleich** `prev_val`, addieren wir ihn regulär zur Gesamtsumme.
- Wir aktualisieren `prev_val = current_val`.

```mermaid
graph RL
    V["V (5)"] -->|prev_val = 5| I["I (1): 1 < 5 -> Minus!"]
    I --> Res["total: +5 - 1 = 4"]

    style V fill:#3f51b5,stroke:#fff,stroke-width:2px,color:#fff
    style I fill:#f44336,stroke:#fff,stroke-width:2px,color:#fff
    style Res fill:#4caf50,stroke:#fff,stroke-width:2px,color:#fff
```

---

## Implementierung (Python 3)

```python
class Solution:
    def romanToInt(self, s: str) -> int:
        """Konvertiert eine römische Zahl in eine Ganzzahl.

        Args:
            s: Gültiger String einer römischen Zahl

        Returns:
            Ganzzahliger Wert
        """
        roman_map = {
            "I": 1,
            "V": 5,
            "X": 10,
            "L": 50,
            "C": 100,
            "D": 500,
            "M": 1000,
        }

        total = 0
        prev_val = 0

        # Von rechts nach links durch den String laufen
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

## Komplexitätsanalyse

| Dimension | Komplexität | Begründung |
| :--- | :--- | :--- |
| **[Zeitkomplexität](../glossary/o-notation.md)** | $\mathcal{O}(n)$ | Wir durchlaufen den String der Länge $n$ genau einmal. Da $n \le 15$ für alle römischen Zahlen bis 3999 gilt, ist die Laufzeit faktisch $\mathcal{O}(1)$. |
| **[Speicherkomplexität](../glossary/o-notation.md)** | $\mathcal{O}(1)$ | Feste [Hash Map](../glossary/hash-map.md) mit 7 Einträgen und zwei Integer-Variablen. |

---

## Edge Cases & Fallstricke

- [x] **Subtraktionen aufeinanderfolgend:** Z. B. `"MCMXCIV"`: Von rechts nach links: V (+5), I (-1), C (+100), X (-10), M (+1000), C (-100), M (+1000) $\to 1994$.
- [x] **Ein einzelnes Zeichen:** Z. B. `"I"` liefert direkt 1.
- [x] **Nur additive Zeichen:** Z. B. `"III"` oder `"VIII"` werden fortlaufend addiert.
