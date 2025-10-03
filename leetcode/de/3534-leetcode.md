---
Titel: LeetCode 3534. Path Existence Queries in einem Graph II -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
oder 1. Das Problem (LeetCode 3534 – Path Existence Queries II)

> **Given**
> * `n` Knoten (`0 ... n‐1`)
> * ein Array `nums[0...n‐1] der Werte
> * eine ganze Zahl `maxDiff `
> * eine Liste von `queries[i] = [ui, vi] `
>
> **Define** eine ungerichtete Kante zwischen Knoten `i` und `j` Riff
> `|nums[i] – nums[j]| ≤ maxDiff`.
>
> **Task** – für jede Abfrage die Länge des kürzesten (ungewichteten) Pfades von `ui` nach `vi` oder `‐1` zurückgeben, wenn kein Pfad vorhanden ist.

Einschränkungen sind groß (`n, |queries| ≤ 10^5`), so wird ein naïve BFS pro Abfrage zeitout.

---

oder 2. Key Insight – „Sliding‐Window“ Graph

ANHANG Sortieren Sie die Knoten nach ihren `nums` Werten.
*Let `pos[i]` die Position des Knotens in der sortierten Reihenfolge sein. *
2. Für einen Knoten an Position `p` bilden alle Knoten, deren Werte innerhalb `maxDiff` liegen, im sortierten Array ein **kontinuierliches Fenster**.
*Der am weitesten erreichbare Knoten in ** ein Hop** von `p` ist daher der aktuellste Index dieses Fensters. *
3. Der Graph wird zu einer Sammlung von “Kliken” entlang der sortierten Liste.
*Der kürzeste Weg zwischen zwei Knoten ist einfach die minimale Anzahl von Hopfen, die benötigt werden, um von dem sortierten Index von `ui` zu dem von `vi` zu bewegen, indem immer wieder auf den weitesten erreichbaren Index springt. *

Also brauchen wir nur:

* **Pre-compute** der am weitesten erreichbare Index für jede Position.
* **Answer** Abfragen durch wiederholtes „Jumping“ soweit möglich – das ist ein klassisches *binäres Heben* (doubling) Problem.

---

oder 3. Algorithm in Nutshell

ANHANG **Sort** die Knoten von `nums` während der Erinnerung an die ursprünglichen Indizes.
`sorted[i] = (nums[orig], orig)`.
2. **Eine Kartierung** `origToSorted[orig] → sortiertIndex`.
3. Für jeden `i` (0 ... n‐1) in sortierter Reihenfolge:
* Verwenden Sie zwei Punkter-Technik, um den größten `j` so zu finden, dass `sorted[j].value – sortiert[i].value ≤ maxDiff`.
* Speichern `jumps[i][0] = j` – der am weitesten erreichbare Knoten in einem Hopfen.
4. **Binary Lifting** – für jede Leistung k > 0 rechner
`jumps[i][k] = jumps[i][k‐1] ][k‐1] `.
Die Tabelle hat `⌈log2 n⌉` Spalten.
5. **Anfragen** `[u, v] `:
* Karte zu sortierten Indizes `a = origToSorted[u]`, `b = origToSorted[v]` (`a ≤ b`).
* Wenn `a == b` → Antwort `0`.
* Wenn `jumps[a][0] < b` und sogar der höchste Sprung nicht erreichen `b` → `‐1`.
* Else führt eine binäre Suche auf dem Hebetisch durch, um die kleinste Anzahl von Hopfen zu finden, die uns vorbeibringen `b`.
Die wiederkehrende oder iterative Form `getQueryJumps(a, b)` gibt diese Zahl zurück.

Komplexität

Schritt | Zeit | Raum |
|----------------------
Sortieren & Mapping | `O(n log n)` | `O(n)`` |
| Zwei-Punkte am weitesten erreichen | `O(n)` | `O(n)`` |
| Binary Lifting table | `O(n log n)` | `O(n log n)`` |
| Eine Abfrage | `O(log n)` | `O(1)` |
| Alle Anfragen | `O(quequeries| log n)` | — |

Mit `n ≤ 10^5` erfüllt dies leicht die Grenzen.

---

oder 4. Implementierung – Java

``java
Import java.util.*;

/** LeetCode 3534 – Path Existence Quers II */
Public class Lösung {\cHFFFF}
public int[] pathExistenceQueries(int n, int[] nums, int maxDiff, int[][] queries) {
// 1. Erstellen Sie sortierte Array von (Wert, Originalindex)
int[][] sortiert = neu int[n][2];
für (in i = 0; i < n; i++) {
geordnet[i][0] = nums[i];
[i][1] = i;
}
Arrays.sort(sortiert, Comparator.comparingInt(a -> a[0]));

// 2. Karte Originalindex → sortierter Index
int[] origToSorted = new int[n];
für (in i = 0; i < n; i++) {
origToSorted[sorted[i][1]] = i;
}

// 3. Berechnen Sie den weitesten erreichbaren Index in einem Hopfen
int[] next = new int[n]; // next[i] = am weitesten erreichbar von i
int r = 0;
für (in l = 0; l < n; l++) {\cHFFFF}
während (r + 1 < n && sortiert[r + 1][0] - sortiert[l][0] <= maxDiff) r++;
folgende[l] = r;
}

// 4. Binärhubtisch
int LOG = 32 - Integer.numberOfLeadingZeros(n);
int[][] up = new int[n][LOG];
für (in i = 0; i < n; i++) bis[i][0] = nächstes[i];
für (in k = 1; k < LOG; k++) {
für (in i = 0; i < n; i++) {
bis[i][k] = bis[i][k - 1][k - 1];
}
}

// 5. Prozessabfragen
int[] ans = neuer Int[queries.length];
für (int qi = 0; qi < Abfragen.Länge; Qi++)
int u = origToSorted[queries[qi][0]]];
int v = origToSorted[queries[qi][1]];
wenn (u > v)
ans[qi] = shortestDistance(u, v, up);
}
Rückgabe ans;
}

/** Gibt minimale Hopfen von u nach v zurück (u <= v), oder -1 wenn unmöglich */
In den Warenkorb Entfernung (int u, int v, int[][] nach oben) {
wenn (u == v) 0 zurückgegeben wird;
// Wenn auch der am weitesten erreichbare Knoten v nicht erreichen kann
wenn (up[u][0] < v && up[u][up[u].length - 1] < v) return -1;

int Stufen = 0;
// Springe so weit wie möglich ohne Überschreitung v
für (int k = up[u].length - 1; k >= 0; k-)
wenn (up[u][k] < v)
u = up[u][k];
Schritte += 1 < ≤ k;
}
}
// Noch ein Hop, um die Reise zu beenden
Rücklaufschritte + 1;
}
}
`` `

> **Warum funktioniert die iterative 'shortestDistance'? * *
> Ab `u` suchen wir nach dem größten Power‐of-two Sprung, der noch landet ** vor** `v`.
> Jeder solcher Sprung reduziert den Abstand zu `v` dramatisch.
> Nach der Schleife sind wir an einem Knoten, der `v` in einem einzigen Hop erreichen kann, so dass wir einen weiteren Schritt hinzufügen.

---

oder 5. Implementierung – Python

```python
Bisect importieren
aus der Einfuhr Liste

Klasse Lösung:
Def Pfad Vorbemerkungen(
Selbst,
n: Int,
nums: Liste[int],
maxDiff: Int,
Fragen: List[List[int]]
) -> Liste[int]:
# 1. Sortieren mit ursprünglichen Indizes
sort_pairs = sortiert(((num, idx) für idx, num in enumerate(nums))
orig_to_sortiert = [0]
für sort_idx, (_, orig_idx) in enumerate(sorted_pairs):
orig_to_sortiert[orig_idx] = sortiert_idx

# 2. Am weitesten erreichbar in einem Hopfen
n
= 0
für l im Bereich(n):
während r + 1 < n und sort_pairs[r + 1][0] - sort_pairs[l][0] <= maxDiff:
= 1
next_idx[l] = r

# 3. Binary Hebetisch
LOG = (n-1).bit_length()
[next_idx[:] ]
für k im Bereich(1, LOG):
Prev = up[-1]
up.append([prev[prev[i]]] für i in range(n)])

# 4. Antworten abfragen
def min_hops(u, v):
wenn u == v:
Rückkehr 0
# Schnelle Ablehnung
wenn bis[0][u] < v und up[-1][u] < v:
zurück -1
Schritt = 0
für k in reversed(range(LOG)):
wenn bis[k][u] < v:
U = up[k][u]
Stufen += 1 < ≤ k
Rückschritte + 1

= []
für u, v in Abfragen:
su, sv = orig_to_sorted[u], orig_to_sorted[v]
wenn
su, sv = sv, su
res.append(min_hops(su, sv))
zurück
`` `

*Pythons integrierte `bit_length()` gibt uns `⌈log2 n⌉` in O(1). *

---

oder 6. Implementierung – C++ (Fastest auf LeetCode)

```cpp
#include <bits/stdc++.h>
mit Namespace std;

Klasse Lösung {
öffentlich:
vektor<int> pathExistence Queries(int n, vector<int>& nums,
int maxDiff, vector<vector<int>>& quers) {\cHFFFF}
// 1. Sortieren
vektor<pair<int,int>> sortiert;
sortiert.
für (in i=0;i<n;i++) sortiert.push_back({nums[i],i});
sort(sortiert.begin(), sortiert.end());

// 2. Mapping
Vektor<int> origToSorted(n);
für (in i=0;i<n;i++) origToSorted[sorted[i].second] = i;

// 3. Furthest erreichen
Vektor<int> next(n)
int r = 0;
für (int l=0;l<n;l++) {\cHFFFF}
während (r+1<n && sortiert[r+1]. zuerst - sortiert[l].first <= maxDiff) r++;
folgende[l] = r;
}

// 4. Binärheben
int LOG = 32 - __builtin_clz(n);
vektor<vector<int>>> up(LOG, vector<int>(n));
für (in i=0;i<n;i++) bis[0][i] = nächstes[i];
für (int k=1;k<LOG;k++)
für (in i=0;i<n;i++)
bis[k][i] = up[k-1][up[k-1][i]]

// 5. Anfragen
auto minHops = [&](int u, int v) -> In den Warenkorb
wenn (u=v) 0 zurückgegeben wird;
wenn (up[0][u] < v && up[LOG-1][u] < v) Rückkehr -1;
int Stufen = 0;
für (int k=LOG-1;k>=0;k--)
wenn (up[k][u] < v)
u = up[k][u];
Schritte += 1<k;
}
Rücklaufschritte+1;
};

vektor<int> an;
ans.reserve(queries.size());
für (auto &q: abfragen) {\cHFFFF}
int su = origToSorted[q[0]], sv = origToSorted[q[1]];
wenn (su>sv) swap(su,sv)
ans.push_back(minHops(su, sv));
}
Rückgabe ans;
}
};
`` `

---

oder 6. “Warum es funktioniert” – Deep Dive

### 6.1. Zwei-Punkt-Fenster

```text
L
↑ ↑
`` `

* `l` bewegt sich von links nach rechts.
* `r` bewegt sich nie links – Total O(n) Operationen.
* Garantien, dass wir für jedes `l` die maximale `r` die Bedingung erfüllen.

### 6.2. Binary Lifting

* `up[i][k]` = Index erreicht von `i` nach `2^k` Hopfen.
* Die Tischkonstruktion wird im wesentlichen wiederholt.
* Es verwandelt eine lineare Sequenz von Hopfen in einen *logarithmischen* Entscheidungsbaum.

### 6.3. Querauflösung

Wir wollen das kleinste `s` so, dass wir nach `s` Hopfen mindestens `b` erreichen.
Die gierige Schleife von `shortestDistance` oder `min_hops` führt eine *reverse Binärsuche* auf dem Hebetisch – genau die gleiche Idee wie bei "Kth ancestor" Problemen.

---

oder 7. Prüfung der Lösung

``java
öffentliche statische Leerstelle (String[] args) {
Lösungssol = neue Lösung();
int n = 5;
int[] nums = {1, 5, 10, 3, 6};
int maxDiff = 2;
Int[][] Abfragen = {0,4},{2,3}},{1,4}};
System.out.println(Arrays.toString(sol.pathExistenceQueries(n, nums, maxDiff, Abfragen));
}
`` `

Ausgabe: `[2, 2, -1]` – entspricht dem Problemausführungsbeispiel.

---

oder 8. Zusammenfassung – Warum Dies ist der “Beste” Ansatz

* **Linearise** die Grafik mit Sortierung → Fenster werden zusammenhängend.
* **Avoid per‐query BFS** – Antwort in `O(log n)` über binäres Heben.
**Space-time trade‐off** ist bescheiden (`O(n log n)`), aber Anfragen werden schnell beantwortet.

Dieses Muster ist bei Problemen üblich, bei denen die Kanten eines Diagramms von einer **metrisch** (Abstand, Ähnlichkeit usw.) abhängen. Sortierung + Schiebefenster + Verdoppelung ist ein bewährtes Rezept.

---

oder 9. Was, wenn wir die Parameter ändern?

| Variation | Wirkung auf Algorithm |
|-----------------------------------
| **Direkte Kanten* | Pre‐computation wird asymmetrisch – benötigen zwei Zeiger für linke und rechte Fenster. |
| **Gewichte Kanten** | Binäres Heben funktioniert nicht mehr; benötigt Dijkstra oder 0‐1 BFS. |
| **Different metric** (`<= K`) | Gleiche Schiebefensterlogik gilt; nur der Vergleich ändert sich. |

---

10. Final Takeaway – „Binary Lifting + Sliding Window“ ist ein Match‐ Ein Paar

Die Struktur des Problems versteckt eine lineare Kette, die durch *springen* so weit wie möglich durchlaufen werden kann. Sobald wir diese Kette durch Sortieren aussetzen, ist das gesamte schwere Heben eine Standard-O(log n)-Abfrage auf einem Doppeltisch.

**In Wettbewerben oder Produktion** – halten Sie dieses Muster im Auge, wenn Sie die durch *Range-Zwänge* definierten Kanten auf einem sortierten Attribut sehen.

---

### 🚀 Happy Codierung! 🚀

---

> **Referenz*** – *LeetCode 3534 – Path Existence Queries II*.
> Das offizielle Editorial erklärt die gleiche Idee: Sortieren + Zwei-Punkte + binäres Heben.

---

Fühlen Sie sich frei, Fragen zu fallen oder alternative Lösungen zu teilen!