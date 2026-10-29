# LeetCode 2791: Count Paths That Can Form a Palindrome in a Tree

- **Schwierigkeit:** Hard 🔴
- **Themen:** Tree, Graph, DFS, Bit Manipulation, Hash Map, Prefix XOR
- **Verwandte Konzepte:** [Adjazenzliste](../glossary/adjazenzliste.md)

---

## 📝 Aufgabenstellung

Gegeben ist ein gewurzelter Baum mit $n$ Knoten (nummeriert von $0$ bis $n - 1$), dessen Wurzel der Knoten $0$ ist.

Der Baum wird beschrieben durch:
- ein Array `parent` der Länge $n$, wobei `parent[i]` der Elternknoten von Knoten $i$ ist (`parent[0] == -1`).
- einen String `s` der Länge $n$, wobei `s[i]` das Zeichen auf der Kante zwischen Knoten $i$ und `parent[i]` ist (`s[0]` wird ignoriert).

Gesucht ist die Anzahl der Knotenpaare $(u, v)$ mit $u < v$, sodass die Zeichen entlang des einfachen Pfades von $u$ nach $v$ zu einem **Palindrom umgeordnet werden können**.

---

## 💡 Intuition & Kernideen

### 1. Wann lässt sich ein String zu einem Palindrom umordnen?
Eine Zeichenkette lässt sich genau dann zu einem Palindrom anordnen, wenn:
- **höchstens ein Buchstabe** eine ungerade Häufigkeit hat (alle anderen Buchstaben kommen mit gerader Häufigkeit vor).

Da `s` nur aus 26 Kleinbuchstaben (`'a'` bis `'z'`) besteht, reicht es völlig aus, für jeden Buchstaben nur die **Parität** (gerade = 0, ungerade = 1) zu kennen.

### 2. Bitmask für 26 Buchstaben
Wir repräsentieren die Paritäten der 26 Buchstaben in einer einzigen 26-Bit-Ganzzahl (`mask`):
- Bit $k$ steht für den Buchstaben `'a' + k`.
- Taucht der Buchstabe ein weiteres Mal auf, invertieren wir Bit $k$ mittels XOR:
  $$\text{mask} \oplus (1 \ll k)$$

### 3. Pfad zwischen zwei Knoten via Prefix-XOR
In einem Baum verläuft der Pfad zwischen $u$ und $v$ über ihren kleinsten gemeinsamen Vorfahren (LCA):
$$\text{Pfad}(u, v) = \text{Pfad}(\text{Root}, u) \oplus \text{Pfad}(\text{Root}, v)$$

Die Kanten vom Wurzelknoten zum LCA liegen auf beiden Wegen und heben sich im XOR gegenseitig auf ($x \oplus x = 0$).

Damit der Pfad zwischen $u$ und $v$ ein Palindrom bilden kann, muss für die Bitmasken gelten:
$$\text{mask}(u) \oplus \text{mask}(v) \in \{0, 2^0, 2^1, \dots, 2^{25}\}$$

Das entspricht genau zwei Fällen:
1. **$\text{mask}(u) == \text{mask}(v)$:** Alle Zeichen auf dem Pfad kommen mit gerader Häufigkeit vor (Ergebnis 0).
2. **$\text{mask}(u) \oplus \text{mask}(v) == (1 \ll k)$:** Genau ein Buchstabe kommt mit ungerader Häufigkeit vor (die Masken unterscheiden sich in genau einem Bit).

---

## 🐍 Implementierung (Python)

Wir bauen den Baum als [Adjazenzliste](../glossary/adjazenzliste.md) auf, ermitteln per Tiefensuche (DFS) für jeden Knoten seine Bitmaske bezüglich der Wurzel und zählen passende Paare über eine Hash Map (Frequenz-Zähler) analog zum 2-Sum-Prinzip.

```python
from collections import Counter
from typing import List


class Solution:
    def countPalindromePaths(self, parent: List[int], s: str) -> int:
        n = len(parent)

        # 1. Adjazenzliste des Baums aufbauen: parent -> [(child, bitmask)]
        tree = [[] for _ in range(n)]
        for i in range(1, n):
            p = parent[i]
            char_bit = 1 << (ord(s[i]) - ord("a"))
            tree[p].append((i, char_bit))

        # 2. DFS: Masken von der Wurzel zu jedem Knoten berechnen
        # masks[u] = Bitmaske der Kantenzeichen auf dem Pfad 0 -> u
        masks = [0] * n

        def dfs(node: int, current_mask: int) -> None:
            masks[node] = current_mask
            for child, bit in tree[node]:
                dfs(child, current_mask ^ bit)

        dfs(0, 0)

        # 3. Paare zählen via Counter (Prefix-Frequenzen)
        count = Counter()
        ans = 0

        for mask in masks:
            # Fall 1: Genau dieselbe Maske -> alle Zeichen geradzahlig
            ans += count[mask]

            # Fall 2: Masken unterscheiden sich um genau 1 Bit (ein Zeichen ungerade)
            for k in range(26):
                ans += count[mask ^ (1 << k)]

            count[mask] += 1

        return ans
```

---

## 📊 Komplexitätsanalyse

| Dimension | Komplexität | Erklärung |
| :--- | :--- | :--- |
| **Zeitkomplexität** | $\mathcal{O}(26 \cdot n) = \mathcal{O}(n)$ | Baumaufbau $\mathcal{O}(n)$, DFS $\mathcal{O}(n)$, Zählen der Paare benötigt für jeden Knoten 26 Bit-Checks $\rightarrow \mathcal{O}(26n)$. |
| **Speicherkomplexität** | $\mathcal{O}(n)$ | Adjazenzliste $\mathcal{O}(n)$, Rekursionsstapel $\mathcal{O}(n)$ im Worst-Case (entarteter Baum), Counter & Mask-Array $\mathcal{O}(n)$. |

---

## 💡 Alternativer One-Pass-Ansatz

Man kann die Paare auch direkt *während* der DFS zählen, ohne vorher alle Masken in einem Array zwischenzuspeichern:

```python
from collections import defaultdict
from typing import List


class SolutionOnePass:
    def countPalindromePaths(self, parent: List[int], s: str) -> int:
        n = len(parent)
        tree = [[] for _ in range(n)]
        for i in range(1, n):
            tree[parent[i]].append((i, 1 << (ord(s[i]) - ord("a"))))

        ans = 0
        cnt = defaultdict(int)
        cnt[0] = 1  # Wurzel hat Maske 0

        def dfs(u: int, mask: int):
            nonlocal ans
            for v, bit in tree[u]:
                nxt_mask = mask ^ bit
                ans += cnt[nxt_mask]
                for k in range(26):
                    ans += cnt[nxt_mask ^ (1 << k)]
                cnt[nxt_mask] += 1
                dfs(v, nxt_mask)

        dfs(0, 0)
        return ans
```

---

## ⚠️ Edge Cases & Fallstricke

1. **Rekursionslimit in Python:** Bei $n = 10^5$ und einem linearen Baum (Kette) kann Python an das Standard-Rekursionslimit (`sys.getrecursionlimit()`) stoßen. In der Praxis kann `sys.setrecursionlimit(200000)` oder eine iterative DFS (Stack) nötig sein.
2. **Knoten 0 ignorieren:** `s[0]` hat keine eingehende Kante und muss ignoriert werden; der Index-Shift beginnt erst ab Knoten 1.
3. **Paar-Reihenfolge ($u < v$):** Durch das schrittweise Hinzufügen zum `Counter` (erst `ans += count[...]`, dann `count[mask] += 1`) wird jedes Paar automatisch genau einmal gezählt.
