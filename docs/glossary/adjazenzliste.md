# Adjazenzliste (Adjacency List)

Die **Adjazenzliste** ist eine der wichtigsten und am häufigsten verwendeten Datenstrukturen zur Repräsentation von **Graphen** und **Bäumen** in der Informatik.

---

## 💡 Intuition & Kernidee

Statt wie bei einer Matrix für jedes mögliche Knotenpaar Speicher zu reservieren, merkt sich bei einer Adjazenzliste jeder Knoten **nur die Nachbarn, mit denen er tatsächlich verbunden ist**.

Man kann sich das wie ein Adressbuch vorstellen: Jeder Knoten hat seine eigene Liste an Kontakten (Kanten), die von ihm ausgehen.

```
Graph:
(0) --- [a] ---> (1)
 |
 +---- [b] ---> (2)

Adjazenzliste:
0: [(1, 'a'), (2, 'b')]
1: []
2: []
```

---

## ⚖️ Vergleich: Adjazenzliste vs. Adjazenzmatrix

| Kriterium | Adjazenzliste | Adjazenzmatrix |
| :--- | :--- | :--- |
| **Speicherplatz** | $\mathcal{O}(V + E)$ (optimal für dünne Graphen) | $\mathcal{O}(V^2)$ (verschwenderisch bei wenigen Kanten) |
| **Kante $(u, v)$ existiert?** | $\mathcal{O}(\text{deg}(u))$ bzw. $\mathcal{O}(1)$ mit Set | $\mathcal{O}(1)$ |
| **Alle Nachbarn von $u$ finden** | $\mathcal{O}(\text{deg}(u))$ (direkter Zugriff) | $\mathcal{O}(V)$ (ganze Zeile muss gescannt werden) |
| **Kante hinzufügen** | $\mathcal{O}(1)$ | $\mathcal{O}(1)$ |

> **Faustregel:** In Coding-Interviews und Algorithmen-Wettbewerben (wie LeetCode) sind die meisten Graphen **dünn** ($E \ll V^2$). Eine Adjazenzliste ist daher fast immer die richtige Wahl.

---

## 🐍 Implementierung in Python

In Python lässt sich eine Adjazenzliste besonders elegant mit `collections.defaultdict(list)` oder einer Liste von Listen aufbauen.

### 1. Ungerichteter, ungewichteter Graph

```python
from collections import defaultdict

# Gegebene Kantenliste: (u, v)
edges = [(0, 1), (0, 2), (1, 2), (2, 3)]

graph = defaultdict(list)
for u, v in edges:
    graph[u].append(v)
    graph[v].append(u)  # Da ungerichtet, Kante in beide Richtungen

# Ausgabe:
# graph[0] -> [1, 2]
# graph[1] -> [0, 2]
# graph[2] -> [0, 1, 3]
# graph[3] -> [2]
```

### 2. Gerichteter Graph mit Kantengewichten/-attributen

Häufig tragen Kanten zusätzliche Informationen (z. B. Kosten oder Buchstaben wie in [LeetCode 2791](../solutions/leetcode-2791.md)):

```python
from collections import defaultdict

# Kanten mit Attribut: (u, v, weight)
edges = [(0, 1, "a"), (0, 2, "b"), (1, 3, "c")]

graph = defaultdict(list)
for u, v, weight in edges:
    graph[u].append((v, weight))

# Traversierung der Nachbarn von Knoten 0:
for neighbor, weight in graph[0]:
    print(f"Kante zu {neighbor} mit Label '{weight}'")
```

### 3. Baum aus einem `parent`-Array aufbauen

In Baum-Aufgaben wird der Baum oft über ein Array `parent` spezifiziert, wobei `parent[i]` der Elternknoten von $i$ ist:

```python
parent = [-1, 0, 0, 1, 1, 2]
n = len(parent)

tree = [[] for _ in range(n)]
for child in range(1, n):
    p = parent[child]
    tree[p].append(child)

# tree[p] enthält jetzt alle direkten Kinder von Knoten p
```

---

## 🔍 Typische Anwendungsfälle

- **Tiefensuche (DFS)** und **Breitensuche (BFS)** (z. B. Zusammenhangskomponenten, kürzeste Wege in ungewichteten Graphen).
- **Dijkstra-Algorithmus** für kürzeste Pfade mit Gewichten.
- **Topologische Sortierung** auf gerichteten, kreisfreien Graphen (DAGs).

---

## ⚠️ Stolpersteine

1. **Gerichtet vs. Ungerichtet:** Bei ungerichteten Graphen darf `graph[v].append(u)` nicht vergessen werden – sonst ist der Graph unvollständig.
2. **KeyError bei einfachen Dictionaries:** Ein normales `dict` wirft einen Fehler, wenn ein Knoten keine ausgehenden Kanten hat. `defaultdict(list)` oder eine vorbereitete Liste `[[] for _ in range(n)]` verhindert dies.
3. **Knoten ohne Kanten:** Isolierte Knoten tauchen in einer reinen Kantenliste eventuell gar nicht auf. Bei fester Knotenzahl $n$ ist `[[] for _ in range(n)]` die sicherste Variante.
