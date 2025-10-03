---
Titel: LeetCode 1439. Finden Sie das Kth Smallest Sum einer Matrix mit sortierten Reihen -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
oder 1. Das Problem

> **LeetCode 1439 – Finden Sie das Kth Smallest Sum einer Matrix mit sortierten Rows* *
> ** Schwierigkeit**: schwer

Sie erhalten eine `m × n` Matrix `mat`, deren Zeilen in nicht abnehmender Reihenfolge sortiert sind.
Aus jeder Zeile müssen Sie **genau ein ** Element auswählen, das eine Reihe von Länge `m` erzeugt.
Unter allen möglichen Arrays benötigen Sie die **kth kleinste Summe* ihrer Elemente.

`` `
Eingang
Matt = [[1,3,11],
[2,4,6]
k = 5

Ausgangsleistung
7
`` `

Die ersten fünf kleinsten Summen sind
`[1,2] → 3`, `[1,4] → 5`, `[3,2] → 5`, `[3,4] → 7`, `[1,6] → 7`.
Die 5. Summe ist `7`.

`1 ≤ m,n ≤ 40`, `1 ≤ k ≤ min(200, m*n)`, `1 ≤ mat[i][j] ≤ 5000`.



------------------------------------------------------

oder 2. Die Idee – „Keep the Best k Sums“

Die Anzahl aller möglichen Summen kann astronomische groß sein (`n^m`).
Weil **k winzig ist (≤ 200)* können wir vermeiden, alles aufzuzählen.

**Key Observation**
Wenn Sie die ersten `i` Zeilen verarbeitet haben, benötigen Sie nur die *k kleinste* Teilsummen.
Jede Summe, die nicht unter diesen k ist, kann nie Teil einer letzten k‐ten kleinsten Summe werden –
es wäre bereits größer als mindestens k andere Teilsummen.

So iterieren wir Zeile für Zeile, wobei ein *max‐Hap von Größe maximal k*, die immer
speichert die bisher gesehen kleinsten Summen.
Wenn eine neue Zeile ankommt, kombinieren wir jede aktuelle Teilsumme mit jedem Element von
diese Zeile und schieben die neuen Summen in einen neuen Haufen, verwerfen die größten, so dass die
Größe überschreitet nicht k.

Der Algorithmus ist:

`` `
heap ← [0] // eine Summe vor der Bearbeitung von Zeilen
für jede Zeile r in Matte:
neue Heap ← leer max-heap
für jede Summe s im Haufen:
für jedes Element v in ersten min(k, n) Elementen von r:
newHeap.push(s + v)
wenn neuHeap.size > k:
newHeap.pop() // das größte entfernen
heap.de

zurück heap.top() // die k‐te kleinste Summe
`` `

Da jede Zeile höchstens `k` relevante Spalten hat (`k` ≤ 200), sind die inneren Schleifen
sehr klein.
Zeitkomplexität: **O(m · n · k · log k**
Raumkomplexität: **O(k)*

Die gleiche Idee kann mit einem *min‐heap* realisiert werden, wenn Sie zuerst alle generieren
Kandidatsummen und Pop die kleinsten k-male, aber der max‐heap hält den Speicher
Fußabdruck niedrig und gibt die Antwort in einem einzigen Pass.

------------------------------------------------------

oder 3. Code – 3 Sprachen

### 3.1 Java

``java
Import java.util.*;

Public class Lösung {\cHFFFF}
int kthSmallest(int[][] mat, int k) {
int C = Math.min(mat[0].length, k);

// max‐heap: größtes Element oben
Priorität Queue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
maxHeap.add(0); // Startsumme

für (int[] Zeile : mat) {
Priorität Queue<Integer> next = new PriorityQueue<>>(Collections.reverseOrder());

für (int prev : maxHeap) {
für (int c = 0; c < C; ++c) {\cHFFFF}
next.add(prev + Zeile[c));
wenn (next.size() > k next.poll(); // nur k kleinste
}
}
maxHeap = nächstes;
}
maxHeap.peek(); // k‐te kleinste Summe
}
}
`` `

### 3.2 Python

```python
Import heapq
aus der Einfuhr Liste

Klasse Lösung:
def kthSmallest(self, mat: List[List[int]], k: int) -> int:
C = min(len(mat[0]), k)

# max‐heap über negative Zahlen
max_heap = [0] # Start mit Summe 0
für Zeile in Matte:
new_heap = []
für s in max_heap:
für v in Zeile[:C]:
heapq.heappush(new_heap, -(s + v))
wenn len(new_heap) > k:
heapq.heappop(new_heap) # drop Large
max_heap = new_heap

# top of the max‐heap (negativ)
zurück -max_heap[0]
`` `

### 3.3 C++

```cpp
#include <bits/stdc++.h>
mit Namespace std;

Klasse Lösung {
öffentlich:
int kthSmallest(vector<vector<int>& mat, int k)
int C = min((int)mat[0].size(), k);
// max‐heap: prior_queue hält am größten
prior_queue<int> maxHeap;
maxHeap.push(0); // Startsumme

für (const auto& Zeile : mat) {
prior_queue<int> als nächstes;
während (!maxHeap.empty() {\cHFFFF}
int s = maxHeap.top(); maxHeap.pop();
für (in i = 0; i < C; ++i) {
next.push(s) + Zeile[i];
wenn (int)next.size() > k) next.pop(); // halten k kleinste
}
}
maxHeap.swap(nächst);
}
maxHeap.top(); // k‐te kleinste Summe
}
};
`` `

Alle drei Lösungen laufen in **O(m · n · k · log k)** Zeit und verwenden **O(k)* Speicher –
perfekt für die Zwänge (`m, n ≤ 40`, `k ≤ 200`).

------------------------------------------------------

oder 4. Blog Artikel – “Das Gute, Das Schlechte, Die Ugly von LeetCode Hards”

> **Titel**: *Das Gute, das Schlechte und die Ugly von LeetCode Hard Probleme – Ein Job‐Ready Guide*
> **Meta‐description*: Master LeetCode 1439, das Matrix-Puzzle "kth small sum" mit Java-, Python- und C++-Lösungen. Erfahren Sie, wie harte Probleme in Interview gewinnt.
> **Keywords**: LeetCode Hard, 1439, kth kleinste Summe Matrix, Interview Prep, Job Interview, Algorithmus Design, max‐heap, min‐heap, Job Interview Tipps

---

### 🚀 Einführung

Interviewer lieben harte LeetCode Probleme. Sie sind die *Unterschrift* eines guten Ingenieurs.
Aber zeigen sie wirklich Fähigkeiten, oder sind sie nur “Puzzles, die Sie schwitzen”?
Lassen Sie uns es mit einer der am meisten gesprochenen harten Fragen aufbrechen: **LeetCode 1439 – Finden Sie das Kth Smallest Sum einer Matrix mit sortierten Rows*.

> **Warum ist es wichtig*
> * 1439 erscheint in den meisten „Hard“-Interview-Prep-Listen.
* Es zwingt Sie, über **Raum-effizient** Lösungen zu denken, nicht nur brutale Kraft.
> * Mastering it signals you can handle * * Dynamische Programmierung + Heaps* - ein Gold-Mine für Senior-Rollen.

---

### 🔎 Das Gute – Ein hartes Problem in ein Interview verwandeln Gold‐Mine

ANHANG **Klarengpässe* *
*`k ≤ 200`* ist eine winzige Zahl; der Trick ist es zu verwenden.
Interviewer lieben es, wenn Sie erkennen, dass Sie *prune* der Suchraum.

2. ** Wiederverwendbares Muster**
Die Strategie „die besten k sums“ erscheint in
* [LeetCode 373 – Finde K Pairs mit kleinsten Summen](https://leetcode.com/Probleme/find-k-pairs-with-smallest-sums/)
* [LeetCode 373 – K Kleinste Paare](https://leetcode.com/Probleme/k-th-smallest-pair-distanz/)
Ein hartes Problem zu praktizieren lehrt Ihnen ein wiederverwendbares Muster: **max‐Hap von fester Größe**.

3. **Language-agnostische Lösung* *
Alle drei oben genannten Sprachen lösen das gleiche Problem auf die gleiche Weise.
Das ist der perfekte Gesprächspunkt: *“Ich kann saubere, effiziente Java-, Python- und C++-Code schreiben.”*

---

### ❌ The Bad – Common Pitfalls That make you Lose

| Pitfall | Warum es schmerzt | Fix |
|------------------------------
| **Brute Kraftaufzählung** | Exponentially large space → Time‐outs | Verwenden Sie k‐pruning über Haufen |
| **Ignorieren “k ≤ 200”** Kombinieren Sie alle n Elemente → O(n2) pro Zeile | Prozess nur die ersten `min(k, n)` Elemente |
| **Wrong heap type** | Max‐heap-Logik mit min‐heap führt zu O(k2) pop/push | Verwenden Sie max‐heap der Größe k, Pop der Größte bei Überschreitung von |
| **Neglecting edge cases** | Einreihige Matrix, Zeilen mit `n < k` | Griff `m == 1` und `C = min(n, k)` |

Wenn Sie in eine dieser Fallen fallen, wird der Interviewer eine *schwarze Einsicht* sehen.
Eine saubere, speichereffiziente Lösung zeigt algorithmische Reife.

---

### Die Ugly – Welche Interviewer suchen (und wie man es vermeidet)

| Ugly Symptom | Welche Interviewer bemerken | Wie zu beheben |
-------------------------------------------------------------
| **“Ich habe alle Kombinationen ausprobiert, es ist ausgefallen.“* | Zeigt Mangel an *Pruning* Denken | Finde den k‐pruning Trick, nutze einen Haufen |
| **“Ich verwendete Recursion und bekam Stack-Überlauf.”** | Over‐recursive DP ohne Memoization | Verwenden Sie iterative Haufen merging |
| **“Ich gab das falsche Element zurück (min‐heap vs max‐heap).”** | Mis‐Verstehen von Heap Top | Halten Sie ein Maximum von Größe k; geben Sie seine Top |

**Takeaway**: Wenn Sie *erklären* können, warum ein max‐Heap von Größe k funktioniert, sind Sie bereits vor.

---

oder 5. Interview-Ready Tipps

ANHANG **Start mit Einschränkungen* *
*“Weil k ≤ 200, können wir nur die besten k Teilsummen halten.”*
Einschränkungen führen den Lösungsweg.

2. **Erklären Sie die “Warum” vor dem “Wie”* *
Interviewer schätzen Einblicke.
„Wir halten einen max‐Hap, weil keine Summe nicht unter den k kleinsten Teilsummen nicht in der endgültigen Antwort sein kann. „

3. **Weitere alternative Ansätze**
Erwähnen Sie die min‐heap-pairing-Methode, binäre Suche auf der Antwort, etc.
„Hier ist ein zweiter Weg mit einem Min‐Hap von Paaren. „

4. **Zeit/Space
Diskutieren Sie den O(m·n·k·log k) vs. O(m·n·k)-Ansatz, und warum Sie das Maximum gewählt haben.

5. **Schreiben Sie sauberen Code**
*Deskriptive Variablennamen*, *Inline-Kommentare*, *Typ-Annotationen* (Python 3.9+).
Interviewer überprüfen Lesbarkeit genauso wie Korrektheit.

6. **Practice Edge Cases*
*Einzelzeile, einzelne Spalte, alle gleichen Werte, k = m*n. *
Seien Sie bereit, schnelle Tests auf eigene Faust durchzuführen.

7. **Relate to real life* *
„In der Produktion benötigen Sie oft die k‐smallest Werte aus sortierten Streams – dieser Algorithmus ist derselbe. „

---

oder 6. Wörter schließen – Den Job bekommen

*Hard-Probleme wie LeetCode 1439 sind nicht nur Puzzles; sie sind ein **testing Ground** für Ihre Design-Instinkte. *
Wenn Sie durchgehen können:

* Die **constraints* → „Weil k klein ist... „
* Die **core-Idee** → „Keep the best k sums“
* Die **clean Implementation** → “Java, Python, C++”

Sie werden die Qualitäten zeigen, die Manager wollen: **algorithmisches Denken, Liebe zum Detail und die Fähigkeit, produktionsbereiten Code* zu schreiben.

Also nächstes Mal sehen Sie ein hartes Problem, erinnern Sie sich:
**Good*** – Sie sehen ein Muster.
**Bad** – Sie verschwenden Zeit aufzählen alles.
**Ugly** – Sie irrtümliche Datenstrukturen.

Vermeiden Sie die schlechten und hässlichen; üben Sie das Gute, und Sie werden bereit sein, dieses Interview zu ace und landen den Job. Glückliche Kodierung!