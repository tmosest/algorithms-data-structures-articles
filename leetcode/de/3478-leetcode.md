---
Titel: LeetCode 3478. Wählen Sie K Elemente Mit maximaler Summe -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
oder 1. Problem Recap

**LeetCode 3478 – Wählen Sie K Elemente Mit maximaler Sum**

*Input*
`nums1`, `nums2` – zwei ganze Arrays der Länge `n `
`k` – eine positive Ganzzahl (`1 ≤ k ≤ n`)

*Task*
Für jeden Index `i` (0-basiert):

ANHANG Alle Indizes `j` finden, so dass `nums1[j] < nums1[i]`.
2. Aus diesen Indizes wählen Sie ** höchstens* `k` Werte von `nums2[j]` die die maximal mögliche Summe geben.
3. Speichern Sie diese Summe in `answer[i]`.

Gibt das Array `answer` zurück.

*Beschränkungen*
`1 ≤ n ≤ 105`
`1 ≤ nums1[i], nums2[i] ≤ 106`

Die klassische Lösung verwendet ein **sort + min‐heap** (Priority queue) und läuft in `O(n log n)` Zeit und `O(k)` Extra-Raum.

Im Folgenden finden Sie saubere, gut ausgestattete Implementierungen in **Java, Python und C++**.

---

oder 2. Kernidee

ANHANG **Sort by `nums1`.**
Wenn das Array zunehmend sortiert wird, hat jedes Element, das wir bereits verarbeitet haben, einen `nums1`-Wert * enger kleiner * als das aktuelle.
Die einzige Nuance: Duplikate dürfen nicht als „kleiner“ betrachtet werden. Wir lösen dies, indem wir gleiche Werte gruppieren.

2. ** Halten Sie einen Min‐Hap des besten `k` `nums2` bisher gesehen. **
- Der Haufen speichert die *k größten* `nums2` Werte aufgetreten.
- `sum` hält die aktuelle Summe der Haufeninhalte.
- Wann immer ein neuer `nums2`-Wert eingefügt wird, drücken wir ihn; wenn der Haufen über `k` wächst, legen wir den kleinsten Wert und subtrahieren ihn von `sum`.
So ist `sum` immer die maximale Summe von maximal `k` Elementen, die aus Indizes mit einem kleineren `nums1` kommen.

3. **Antwort für eine Gruppe von `nums1`**
Für jeden Index in der Gruppe vergeben wir den aktuellen `sum`.
Nur wenn alle Antworten für die Gruppe gesetzt sind, fügen wir die `nums2` Werte der Gruppe zum Haufen hinzu (so werden sie nicht für sich selbst gezählt).

---

oder 3. Implementierung

### 3.1 Java

``java
Import java.util.*;

/**
* LeetCode 3478 – Wählen Sie K Elemente mit maximaler Summe
*
Klasse Lösung {
öffentlich long[] findMaxSum(int[] nums1, int[] nums2, int k) {
int n = nums1.Länge;
lange[] Antwort = neue lange[n];

// Paar jedes Element mit seinem ursprünglichen Index
int[][] paar = neu int[n][2];
für (in i = 0; i < n; i++) {
paar[i][0] = nums1[i]; // Wert für Sortierung
paar[i][1] = i; // Originalindex
}

// Sortieren nach nums1 aufsteigend
Arrays.sort(Paare, Comparator.comparingInt(a -> a[0]));

// min-heap für die k größten nums2 Werte bisher gesehen
Priorität Queue<Integer> heap = new PriorityQueue<>;
lange Strömung Summe = 0;

int i = 0;
(i < n)
int j = i;
// das Ende der aktuellen Gruppe finden (alle gleich nums1)
während (j < n && paar[j][0] == paar[i][0]) j++;

// 1️⃣ Antwort für jeden Index in der Gruppe verwendet den aktuellen Summe
für (int t = i; t < j; t++) {\cHFFFF}
Antwort[Paare[t][1]] = currentSum;
}

// 2️⃣ füge nun die nums2 -Werte dieser Gruppe zum Haufen hinzu
für (int t = i; t < j; t++) {\cHFFFF}
int idx = paar[t][1];
int val = nums2[idx];
heap.offer(val);
Strom Summe + = val;

// nur die k größten Werte halten
wenn (Hap.size() > k) {\cHFFFF}
Strom Summe -= heap.poll();
}
}

i = j; // zur nächsten Gruppe wechseln
}

Antwort zurück;
}
}
`` `

### 3.2 Python

```python
aus heapq import heappush, heappop
aus der Einfuhr Liste

Klasse Lösung:
def findMaxSum(self, nums1: List[int], nums2: List[int], k: int) -> Liste[int]:
n = len(nums1)
Antwort = [0] * n

# Paarwert mit Originalindex
paare = sortiert([(val, idx) für idx, val in enumerate(nums1)], key=lambda x: x[0])

Heap = [] # min‐heap of best k nums2 value
Strom_sum = 0
= 0
während i < n:
j = i
während j < n und Paare[j][0] == Paare[i][0]:
: 1

# Antworten für diese Gruppe
für t im Bereich (i, j):
Antwort[Paare[t][1]] = current_sum

# add group's nums2 to the heap
für t im Bereich (i, j):
idx = Paare[t] [1]
= nums2[idx]
heappush(heap, val)
Strom_sum += Wert
wenn len(heap) > k:
current_sum -= heappop(heap)

i = j

Antwort
`` `

### 3.3 C++

```cpp
#include <bits/stdc++.h>
mit Namespace std;

Klasse Lösung {
öffentlich:
Vektor<long long> findMaxSum(vector<int>& nums1, vector<int>& nums2, int k) {
int n = nums1.size();
Vektor<long long> ans(n, 0)

// Paar {nums1 Wert, Originalindex}
Vektor<pair<int,int>> paar(n);
für (in i = 0; i < n; ++i) Paare[i] = {nums1[i], i};

sort(pairs.begin(), pair.end(), [](const auto& a, const auto& b){
Rückgabe a.first < bfirst;
})

prior_queue<int, vector<int>, größer<int>> minHeap;
langes CurSum = 0;
int i = 0;
(i < n)
int j = i;
während (j < n && paare[j].first == paar[i].first) ++j; // Gruppe gleich nums1

// 1️⃣ Antwort für die ganze Gruppe geben
für (int t = i; t < j; ++t)
ans[pairs[t].second] = curSum;

// 2️⃣ Fügen Sie die nums2 Gruppe in den Haufen
für (int t = i; t < j; ++t) {\cHFFFF}
int idx = paar[t].second;
int val = nums2[idx];
minHeap.push(val);
curSum += val;
wenn (int)minHeap.size() > k {\cHFFFF}
curSum -= minHeap.top();
minHeap.pop();
}
}

i = j;
}
Rückgabe ans;
}
};
`` `

Alle drei Lösungen laufen in `O(n log n)` Zeit und verwenden `O(k)` Extra-Raum, die bequem zu den Zwängen passt (`n ≤ 105`).

---

oder 4. Blog Post – “Choose K Elemente mit maximaler Summe: Das Gute, das Schlechte & Die Ugly”

> **SEO Keywords*: LeetCode 3478, Wählen Sie K Elemente Maximal Summe, sortbasierter Haufen, Prioritätswarte, Algorithmus-Design, Zeit-Raum-Komplexität, Java, Python, C++-Lösungen

---

### 4.1 Einführung

Wenn Sie Array-basierte Interview-Fragen anpacken, haben Sie wahrscheinlich gesehen * “Pick the best k”* Probleme die ganze Zeit.
LeetCode 3478 bittet Sie, genau das zu tun – aber mit einem zusätzlichen Drall: die Indizes, die Sie wählen können, sind ** durch einen Vergleich auf einem zweiten Array ** eingeschränkt.
In diesem Beitrag gehen wir durch die **good** Lösung, zeigen die **bad** Fallstricke, die häufig Menschen hochfahren und die **ugly** Eck-Fälle aussetzen, die dieses Problem subtil machen.

---

### 4.2 Das „Gute“ – Warum Dieser Ansatz ist elegant

ANHANG **Sorting gibt einen linearen Auftrag für „smaller“* *
Sobald das Array nach `nums1` sortiert ist, erfüllen alle früheren Elemente `nums1[j] < nums1[i]` automatisch – keine teuren Scans erforderlich.

2. **Min‐Hap hält nur die besten k-Zahlen**
Weil der Haufen ein *min* Haufen ist, können wir genau `k` Zahlen in `O(log k)` pro Insertion halten.
Der laufende `sum` gibt Ihnen die Antwort sofort – kein Nachscanning oder Recomputation.

3. **Group‐by‐equal‐value logic**
Duplikate würden sonst eine falsche „kleinere“ Beziehung geben. Die Gruppierung sorgt für Strenge und hält den Algorithmus nach der ersten Sorte linear.

---

### 4.3 Das “Bad” – Häufige Fehler

| Fehler | Warum es zerbricht | Fix |
|-------------------------------
| ** Bei Duplikaten | Indices mit dem gleichen `nums1`-Wert wird ein `<=` Vergleich** für Duplikate | Indices mit dem gleichen `nums1`-Wert als „kleiner“ betrachtet und sich am Ende addiert. | Gruppengleichwerte und Antwort ** vor** Einfügen der Gruppe. |
| ** Jedes Element einzeln vor der Zuordnung von Antworten* | Elemente im aktuellen Index werden in ihrer eigenen Summe gezählt. | Antworten für die ganze Gruppe zuerst zuordnen, dann schieben Sie die Gruppe in den Haufen. |
| ** Verwenden eines Arrays statt eines Haufens** Sie müssen jedes Mal sortieren, wenn Sie das Top-k benötigen, den Algorithmus in `O(nk)` oder schlechter verwandeln. |
| ** Die Annahme k entspricht n** | Der Haufen würde alle Werte halten, aber der Algorithmus funktioniert immer noch; aber die Verwendung eines Haufens in diesem Fall ist Overkill. | Wenn Sie ein superschnelles Kantengehäuse wünschen, können Sie einfach `nums2` sortieren und die top‐k Summe nehmen, aber die generische Lösung bleibt sauber. |

---

### 4.4 The “Ugly” – Edge Cases & Extensions

ANHANG **Sehr groß `k`**
Wenn `k` in der Nähe von `n` ist, wird der Haufen auf diese Größe wachsen; immer noch gut, aber Sie können die Heap Wartung vollständig überspringen, indem Sie die Summe der ersten `k` sortiert `nums2` Werte.
*Komplexität*: `O(n log n)` noch.

2. **Negative Zahlen in `nums2`**
Die Problemaussage garantiert positive ganze Zahlen, aber wenn Sie sich entspannen, wird die “bei den meisten k” Regel wesentlich: Sie können weniger als `k` Elemente wählen, wenn ein negativer Wert reduziert das Gesamt.

3. **Aufsteigen `k` auf der Fliege**
Wenn der Interviewer eine dynamische Version wünscht, in der sich `k` pro Abfrage ändert, braucht man einen ausgewogenen BST oder einen Zwei-Hap-Trick – eine ganz andere Diskussion.

4. **Space-sparende Variante* *
Anstelle eines Haufens können Sie eine sortierte Multimenge der besten `k` Werte (`std::multiset` in C++ oder `SortedList` in Python) behalten.
Die Zeitkomplexität bleibt `O(n log k)`, aber die Konstanten sind etwas größer.

---

### 4.5 Complexity Recap

| Sprache | Zeit | Extra Raum |
|---------------------
| Java | `O(n log n)` | `O(k)`` |
| Python | `O(n log n)` | `O(k)`` |
| C++ | `O(n log n)` | `O(k)` |

Mit `n ≤ 100.000` läuft jede Lösung gut unter einer Sekunde auf typischen Hardware.

---

### 4.6 Letzte Gedanken

LeetCode 3478 ist eine großartige Darstellung, wie **sorting + eine Prioritäts-Warte** ein scheinbar teures "pick the best k" Problem in eine saubere, linear-time Lösung verwandelt.
Durch sorgfältiges Handling von Duplikaten vermeiden wir den häufigsten Fall und bewahren die strenge „<“-Beziehung.

Fühlen Sie sich frei, die Code-Snippets in Ihre lokale IDE zu kopieren, führen Sie die Testfälle und üben Sie den Algorithmus für Variationen (z.B. "pick the best k *greater*" anstelle von "smaller"). Glückliche Kodierung!