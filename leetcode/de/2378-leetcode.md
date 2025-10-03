---
Titel: LeetCode 2378. Wählen Sie Edges, um Score in einem Baum zu maximieren -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
✅ LeetCode 2378 – Wählen Sie Kanten, um den Punkt in einem Baum zu maximieren
**Java | Python | C++** – Komplette Lösungen + **SEO‐optimierter Blog-Post**, der das „gute, schlechte und hässliche“ dieses Problems erklärt, damit Sie Ihr nächstes Codierungsgespräch abhalten können.

---

1️⃣ Problem Recap

Sie erhalten einen **-Wurzelbaum** mit `n` Knoten (0... n‐1).
`edges[i] = [parent_i, weight_i]` (root hat `[-1,-1]`).

Wählen Sie eine Teilmenge von Kanten so aus, dass ** keine zwei ausgewählten Kanten einen Knoten** teilen (d.h. sie sind nicht benachbart).
Maximieren Sie die Summe der Gewichte der gewählten Kanten.
Wenn Sie nichts wählen, ist die Partitur `0`.

> **Beispiele**
> 1. `edges = [[-1,-1],[0,5],[0,10],[2,6],[2,4]] → 11`
> 2. `edges = [[-1,-1],[0,5],[0,-6],[0,7]]] • 7`

---

2️⃣ Warum es ein Medium Problem ist

* **Tree structure** – Sie können nicht gierig auf beliebigen Grafiken verwenden; Sie benötigen ein DP, das die Mutter-Kind-Hierarchie respektiert.
* * **Währungsbeschränkung** – Wahl einer Kante verbietet alle seine einfallenden Kanten, so müssen Sie sich daran erinnern *ob* Sie dürfen eine Kante zu einem Kind wählen.
* **Large n (105)* – O(n2) Lösungen blasen auf; Sie benötigen lineare Zeit.

---

3️⃣ The Core Insight – Tree DP

Denken Sie an jeden Knoten als "Entscheidungspunkt", der in ** zwei Zustände* sein kann:

| Staat | Bedeutung | Was ist erlaubt? |
...
| **0 – “kann nehmen”* | Die Kante vom Stamm des Knotens zu diesem Knoten ** wurde NICHT** gewählt. Sie *kann* eine Kante von diesem Knoten zu einem Kind auswählen. |
| **1 – “kann nicht nehmen”** | Die Kante vom Stamm des Knotens zu diesem Knoten **has* wurde gewählt. Sie *kann* keine Kante von diesem Knoten zu einem Kind (die Eltern haben den Knoten bereits verwendet). |

Für einen Knoten `u`:

`` `
Skip = Summe( Kind[1]  // wir überspringen alle Kanten von u zu seinen Kindern
nehmen = max über Kinder (Kinder[0] - Kind[1] + Gewicht(u,child)
zurück [Skip, nehmen + skip]
`` `

*`skip`* ist die beste Punktzahl, wenn wir **not** keine Kante von `u` nehmen.
*`take`* ist die beste *zusätzliche* Punktzahl, wenn wir beschließen, *genau eine* Kante zu einem Kind zu nehmen (da wir alle Kinder vergleichen).
Schließlich `[skip, take+skip]` Denn wenn der Elternteil diesen Knoten sieht, wird er im Zustand "kann nehmen" (`Skip`) und der Zustand "kann nicht nehmen" ist `take+skip`.

Die Antwort auf den ganzen Baum ist `max(root[0], root[1])`.

Der Algorithmus ist **O(n)*-Zeit, **O(n)*-Speicher (Adjacency List + Recursion Stack).

---

4️⃣ Code Walk‐through – Drei Sprachen

> **Tip**: Die gleiche Idee funktioniert in jeder Sprache. Die einzigen Unterschiede sind Syntax und die Art, wie wir das Diagramm speichern.

---

### 4.1 Java (Java 17+)

``java
Import java.util.*;

Klasse Lösung {
öffentliche lange maxScore(int[][] Kanten) {
int n = Kantenlänge;
Liste<int[]>[] g = neu ArrayList[n];
für (int i = 0; i < n; i++) g[i] = new ArrayList<>();

int root = 0;
für (in i = 0; i < n; i++) {
Int p = Kanten[i][0];
(p >= 0)
g[p].add(neues Int[]{i, Kanten[i][1]}); // Kind, Gewicht
} auch
Wurzel = i;
}
}

long[] res = dfs(root, g); // [canTake, notTake]
zurück Math.max(res[0], res[1]); // beste Punktzahl
}

Private Long[] dfs(int u, List<int[]>[] g) {
long skip = 0; // am besten, wenn wir keine Kante von u
lange Take = 0; // beste *zusätzliche* Punktzahl, wenn wir eine Kante wählen

für (int[] e : g[u]) {\cHFFFF}
lang[] Kind = dfs(e[0, g);
skip +=kind[1]; // Kind muss in "kann nicht nehmen" sein
nehmen = Math.max(take, kind[0] - kind[1] + e[1]); // wähle diesen Rand
}
zurück neue long[]{skip, take + skip}; // beide Staaten zurückgeben
}
}
`` `

---

### 4.2 Python (Python 3.10+)

```python
Import sys
aus Sammlungen import defaultdict
aus der Einfuhr Liste

Klasse Lösung:
def maxScore(self, edges: List[List[int]]) -> int:
sys.setrecursionlimit(1 < < 25)

g = defaultdict(list)
Wurzel = 0
für i, (p, w) in enumerate(edges):
wenn p >= 0:
g[p].append(i, w))
andere:
Wurzel = i

def dfs(u: int):
Skip, Take = 0, 0
für v, w in g[u]:
kind_can, kind_cannot = dfs(v)
Skip += kind_cannot
nehmen = max(take, kind_can - kind_cannot + w)
zurückspringen, nehmen + skip

kann, kann nicht = dfs(root)
zurück max(kann, nicht)
`` `

> **Anmerkung*: `sys.setrecursionlimit` ist erforderlich, da `n` 105 erreichen kann.

---

### 4.3 C++ (C++17)

```cpp
#include <bits/stdc++.h>
mit Namespace std;

Klasse Lösung {
öffentlich:
lange maxScore(vector<vector<int>>>>& Kanten) {\cHFFFF}
int n = Kanten.size();
vektor<vector<pair<int,int>>> g(n); // Kind, Gewicht
int root = 0;
für (in i = 0; i < n; ++i) {\cHFFFF}
Int p = Kanten[i][0];
(p >= 0) g[p].push_back({i, Kanten[i][1]});
andere Wurzel = i;
}

auto dfs = [&](auto&&self, int u.) -> pair<long,long long> {\cHFFFF}
Langer Skip = 0, nehmen = 0;
für (auto [v,w]: g[u]) {\cHFFFF}
auto [child_can, kind_cannot] = self(self, v);
skip += kind_cannot;
nehmen = max(take, kind_can - kind_cannot + w);
}
zurück {skip, nehmen + skip};
};

auto [kann, nicht] = dfs(dfs, root);
zurück max(kann, nicht);
}
};
`` `

---

5️⃣ Komplexitätsanalyse

**Metric*** | **Zeit******
-------------------------
| Gebäude adjacency | `O(n)` | `O(n)`` |
| DFS (ein Pass) | | | | | `O(n)` (Recursion Stack + Adjacency) |

Beide sind optimal für die Zwänge (`n ≤ 105`).

---

6️⃣ Edge‐ Fall Mastering

*****************************
|------------------------------------
| **Alle negativen Gewichte** | Rückgabe negative Zahlen können falsch sein, wenn Sie sich nicht erinnern “0 ist immer erlaubt” | Der DP nimmt automatisch `max(0, ...)` über `skip = 0`. |
| **Roottiefe > 105** | Recursion Stack Overflow | Recursion Limit (Python) erhöhen oder einen expliziten Stack verwenden. |
| **Sehr dichter Baum (viele Kinder)** Die Schlaufe über Kinder bleibt linear, weil jedes Kind genau einmal besucht wird. Keine zusätzlichen Kosten. |
| **Large Gewichte (bis zu 109)** Verwenden Sie `long long` / `long` | Genau wie oben. |

---

Â 6️⃣ Gemeinsames Interview

ANHANG **Miss-Interpreting “adjacent”* – Menschen denken oft nur * zwei* Kanten können nicht gewählt werden, aber in einem Baum * jeder* Rand, der einen ausgewählten berührt, ist verboten.
2. **Die Wurzel vergessen** Wenn Sie das Diagramm mit falschen Richtungen bauen, werden Sie am Ende eine Kante, die bereits von seinem Elternteil genommen.
3. **O(n2) gierig** – Versuche, Kanten nach Gewicht zu sortieren und gierig zu wählen scheitert auf einem Sterndiagramm.
4. **Stack Overflow** – Viele Interviewer führen den Code mit 105 Knoten aus; eine naive Recursion in Java/Python kann die Stacklimits treffen.

---

6️⃣ „Das Gute, das Schlechte und das Böse“

**Aspect********************************
------------------------
| **Algorithmische Effizienz** | Lineare DP auf einem Baum – schnelle und saubere | Recursion Tiefe kann hoch sein | Keine memoization → exponential blow-up |
| **Readability** | Two‐state DP is concise | Das Paar `[skip, take]` kann sich zunächst undurchsichtig fühlen | Verwirrende Variablennamen verweigern oder den Zustand „kann nicht nehmen“ verpassen
| **Skalierbarkeit** | Arbeitet für n=105 | Erfordert erhöhte Rekursionsgrenze | Mit Adjacency-Listen falsch (z.B. `HashMap<Integer, Integer>`) kann Speicher vergeuden
| **Robustness** | Zeigt negative Gewichte automatisch | Benötigt eine sorgfältige Handhabung von 0‐score Fall | Vergessen Sie, dass “Skip” ist bereits das beste für “kann nicht nehmen” kann zur falschen Antwort führen |

---

6️⃣ Tipps für Interview Erfolg

ANHANG ** Starten Sie mit einem Diagramm** – Zeichnen Sie den Baum, markieren Sie die Wurzel und notieren Sie einige Knoten mit den beiden DP-Zuständen.
2. **Erklärung der beiden Staaten vorn** Interviewer lieben es, dass Sie das Problem in klare Unterprobleme brechen.
3. ** Zeige die Übergangsformel** – Schreibe den Pseudo-Code des DFS, übersetze ihn dann.
4. **Run durch ein kleines Beispiel* Schritt durch die DP auf einem 5-Node-Baum, um zu beweisen, dass Sie die Mechaniker verstehen.
5. **Mention the recursion limit* (Python) oder „tail‐recursion / iterative“ Optionen für sehr tiefe Bäume.
6. **Diskuss Randfälle** – All‐negativer, einzelner Knoten, Sternform, ausgeglichener vs. skeweder Baum.

---

7️⃣ Quick‐ Referenz Cheat‐ Blatt

```text
DP[u] = [Skip, Take+Skip]
skip = sum(child[1]) // alle Kinder überspringen
nehmen = max(Kind[0] - Kind[1] + w) // eine Kinderkante auswählen
Antwort = max(DP[root][0], DP[root][1])
`` `

- **Skip** = „Nicht von Eltern verwendet“
- **take** = „keine bereits von Eltern verwendet“
- Nur *ein* Kind kann gewählt werden, weil das Picken einer Kante Blöcke alle anderen.

---

8️⃣ Letzte Gedanken

Dieses Problem ist ein Lehrbuchbeispiel von **tree DP mit Adjacency Zwängen*.
Wenn Sie die Zwei-State-DP artikulieren und in Code übersetzen können, lösen Sie nicht nur das Problem in O(n) Zeit, Sie beeindrucken auch Interviewer mit Ihrem *clean*, *correct* und *well‐commented* Lösung.

Viel Glück! 🚀

---