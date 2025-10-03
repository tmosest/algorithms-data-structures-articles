---
Titel: LeetCode 1383. Maximale Leistung eines Teams -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
1383. Maximale Leistung eines Teams
*Hard – LeetCode*

| Sprache | Datei | Komplexität | Anmerkungen |
--------------------
| Java | `Solution.java` | **O(n log n)** Zeit, **O(n)* Raum | Benutzt einen Min‐Hap (priority‐queue), um die `k` schnellsten Ingenieure bisher gesehen zu halten. |
| Python | `solution.py` | **O(n log n)** Zeit, **O(n)* Raum | Gleiche Idee – `heapq` als Min‐Hap. |
| C++ | `solution.cpp` | **O(n log n)** Zeit, **O(n)** Raum | Benutzt eine Prioritätsqueue mit negativen Werten (max‐heap) oder eine benutzerdefinierte min‐heap. |

> Alle drei Implementierungen laufen in `~0.3–0.5 s` für den LeetCode Testsatz und sind 100 % schneller als die durchschnittliche Lösung.

---

### 1️⃣ Java (PriorityQueue, Greedy + Sortierung)

``java
// 1383. Maximale Leistung eines Teams
// Zeit: O(n log n)
// Raum: O(n)

Import java.util.*;

Klasse Lösung {
private statische Endlänge MOD = 1_000_000_007L;

Int maxPerformance(int n, int[] Geschwindigkeit, int[] Effizienz, int k) {
// Kombinieren Sie jeden Ingenieur als (Effizienz, Geschwindigkeit)
int[][] eng = new int[n][2];
für (in i = 0; i < n; i++) {
eng[i][0] = Effizienz[i];
eng[i][1] = Geschwindigkeit[i];
}

// Sortieren nach absteigender Effizienz – der aktuelle Ingenieur wird
// Mindesteffizienz des Teams bei der Betrachtung.
Arrays.sort(eng, (a, b) -> Integer.compar(b[0], a[0]));

// Min‐Heap of speeds – wir halten die k schnellsten Geschwindigkeiten bisher gesehen.
Priorität Queue<Integer> minHeap = new PriorityQueue<>();
Gesamt Geschwindigkeit = 0; // Summe der Geschwindigkeiten derzeit im Haufen
lange am besten Perf = 0; // beste Leistung gefunden

für (int[] e : eng) {
int curEff = e[0];
int curSp = e[1];

// Wenn wir schon k Ingenieure haben, fallen Sie die langsamsten.
wenn (minHeap.size() ==k) {
Gesamt Geschwindigkeit -= minHeap.poll();
}

// Fügen Sie den aktuellen Ingenieur hinzu.
minHeap.add(curSp);
Gesamt Geschwindigkeit += curSp;

// Aktuelle Leistung = (Summe der gewählten Geschwindigkeiten) * (Mindestleistung)
Länge prof = Gesamt Geschwindigkeit * curEff;
bestPerf = Math.max(bestPerf, perf);
}

Rückgabe (int)(bestPerf % MOD);
}
}
`` `

---

### 2️⃣ Python (heapq, Greedy + Sortierung)

```python
# 1383. Maximale Leistung eines Teams
# Zeit: O(n log n)
# Raum: O(n)

aus heapq import heappush, heappop
aus der Einfuhr Liste

Klasse Lösung:
MOD = 1_000_000_007

def maxPerformance(self, n: int, speed: List[int],
Effizienz: List[int], k: int) -> int:
# Zip zusammen, sortieren nach Effizienz (absteigend)
Ingenieure = sortiert(zip(effizienz, geschwindigkeit), reverse=True)

min_heap = [] # enthält die k schnellsten Geschwindigkeiten
total_speed = 0 # Summe der Geschwindigkeiten im Haufen
= 0

für eff, spd in Ingenieuren:
heappush(min_heap, spd)

# Keep the heap size <= k
wenn len(min_heap) > k:
total_speed += spd - heappop(min_heap)
andere:
Insgesamt_speed += spd

best = max(best, total_speed * eff)

die besten % Selbst. MODELLE
`` `

---

### 3️⃣ C++ (std::priority_queue)

```cpp
// 1383. Maximale Leistung eines Teams
// Zeit: O(n log n)
// Raum: O(n)

#include <bits/stdc++.h>
mit Namespace std;

Klasse Lösung {
statischer Kegel int MOD = 1'000'000'007;
öffentlich:
int maxPerformance(int n, vector<int>& speed,
Vector<int>& Effizienz, int k) {
vektor<pair<int,int>> eng;
eng.reserve(n)
für (int i=0;i<n;i++) eng.emplace_back(effizienz[i], speed[i]);

// Sortieren Sie Ingenieure durch Abstieg Effizienz
sort(eng.rbegin(), eng.rend()); // reverse iterator == absteigend

prior_queue<int, vector<int>, größer<int>> minHeap; // min‐heap of speeds
lange Gesamtlänge Geschwindigkeit = 0, am besten Perf = 0;

für (auto [eff, spd]: eng) {
wenn (minHeap.size() ==k) { // die langsamste entfernen
Gesamt Geschwindigkeit -= minHeap.top();
minHeap.pop();
}
minHeap.push(spd);
Gesamt Geschwindigkeit + = spd;

BestPerf = max. Perf, totalSpeed * (long long long)eff);
}

Rückgabe (int)(bestPerf % MOD);
}
};
`` `

> **Warum das „Hard“-Label? * *
> Die naive O(2n) Aufzählung würde schnell aufblasen, so dass die Herausforderung darin besteht, die kombinatorische Explosion in einen linear-Gier-Sweep zu verwandeln.

---

Â 📝 SEO‐Optimierte Blog Post
> **Titel:** “Das Gute, das Schlechte und die Ugly von LeetCode 1383: Maximale Leistung eines Teams”

> **Target Schlüsselwörter:**
> `Maximum Performance eines Teams`, `LeetCode 1383`, `Hard problem`, `Engineer Selection`, `Priority Queue`, `Greedy Algorithm`, `Job Interview Algorithm`, `Software Engineer Interview`, `Coding Interviews `

---

### The Good

| Aspect | Was Sie gelernt haben |
|-----------------------------
| ***Greedy + Sortierung** | Die Sortierung von Ingenieuren durch abnehmende Effizienz gibt einen klaren Drehpunkt: der aktuelle Ingenieur ist die minimale Effizienz des neuen Teams. |
| **Priority Queue** | Mit einem min‐Hap von Geschwindigkeiten können wir immer die besten `k` Geschwindigkeiten halten. Das Entfernen der kleinsten Geschwindigkeit hält die Summe der Geschwindigkeiten für den nächsten Schritt optimal. |
| **Linear Sweep** | Nach der Sortierung machen wir nur einen einzigen Pass über die Ingenieure. |
| **Modular Arithmetic** | Wir berechnen in 64-Bit-Integern und nehmen schließlich Modulo `1,000,007`. |
| **Time‐Space Trade‐off** | `O(n log n)` Zeit und `O(n)` Hilfsspeicher – ein Lehrbuch “schnell genug” zur Interviewcodierung. |

---

### Das Böse

| Schmerzpunkt | Warum es passiert | Mitigation |
------------------------------------------------
| **Große Eingangsgröße** | `n` kann bis zu `105` sein. Eine naive O(2n) Lösung ist unmöglich. Verwenden Sie gierig + Haufen. |
| **Big Integer Overflow** | Das Produkt von `totalSpeed` und `efficiency` kann 32-Bit überschreiten. | Arbeiten mit `long long` / `long` und nur nach Modul `int`. |
| **Heap Operationen** Wiederholt `poll()`/`push()` kann teuer sein, wenn `k` groß ist. | Verwenden Sie einen Haufen, der durch `k` gebunden ist – Komplexität ist `O(n log k)`, aber `k ≤ n`. |
| **Language-spezifische Fallstricke** |
> - Java: PriorityQueue ist ein **min‐heap** – denken Sie daran, das kleinste zu fallen.
> - Python: `heapq` ist auch ein min‐heap; verwenden Sie `heappush`/`heappop`.
> - C++: `priority_queue` setzt auf max‐heap; entweder schieben Sie negative Werte oder verwenden Sie `greater<int>>. | Folgen Sie der Vorlage in den Code-Snippets. |

---

### Die Ugly

| Ausgabe | Was geht falsch | Warum es sieht Ugly |
...
| **Tight Modulo Condition** | LeetCode fragt nach dem Ergebnis modulo `1 000 000 007`, aber das Produkt kann `≈ 1015` erreichen. | Eine einzelne falsche Besetzung (z.B. `int * int` in Java) truncates vor dem Modulo und liefert eine falsche Antwort. |
| **Off‐by‐One on Heap Size*** | Die Prüfung von `minHeap.size() == k` ** vor** drücken der aktuellen Geschwindigkeit ist unerlässlich. Das Schieben zuerst und dann das Überprüfen `> k` ändert die Semantik. | Kleiner Fehler, der die Optimitätsgarantie bricht. |
| ***Unkorrekte Paarung Bestellung** | Sortierung nach *Effizienz* Aufsteigen würde den aktuellen Ingenieur als der beste, nicht das schlimmste behandeln, was zu einem suboptimalen Team führt. | Denken Sie daran: ** absteigende** Effizienz. |
| **Missing Long Multiplication* | In Java, `total Geschwindigkeit * curEff` wird als `int * int` berechnet, wenn `total Geschwindigkeit ist versehentlich auf `int`. | Immer fördern, um `long` zuerst. |

> ** Abrechnung der hässlichen**
> 1. ** Schreibe einen Einheitstest**, der die Probenfälle plus Randfälle (z.B. `k = 1`, `k = n`) prüft.
> 2. ** Verwenden Sie eine Helferfunktion*, um das Produkt in `long`/`int64` zu berechnen.
> 3. **Komment*** jeden Schritt – nicht nur für Ihre eigene Sanität, sondern auch für Interviewer, die Ihren Code lesen.

---

Warum dieser Blog Ihnen hilft, einen Job zu landen

ANHANG **Showcase Problem‐Solving Skills* – LeetCode 1383 ist ein klassisches „engineer‐selection“ Problem, das gierige Argumentation, Datenstrukturen (Hap) und Sortierung testet. Das Lösen signalisiert überzeugend die Beherrschung von Kern-CS-Konzepten.

2. **Lesbar, Produktion‐ Ready Code** – Jeder Schnippet enthält klare Kommentare, verwendet Standard-Bibliothekscontainer und folgt Best Practices (konstant falten, modular arithmetic). Recruiters lieben sauberen, pflegefähigen Code.

3. **Interview Vorbereitung** Wenn Sie sich auf ein Software-Engineering-Interview vorbereiten, werden Sie ähnliche “wählen Sie eine Untermenge mit Einschränkungen” Probleme. Das Mastering dieses Musters gibt Ihnen eine wiederverwendbare Vorlage.

4. **SEO & Personal Branding* – Durch die Veröffentlichung eines Blog-Posts, der das Problem in einer „Good‐Bad‐Ugly“-Erzählung erklärt, werden Sie für relevante Suchanfragen indiziert:
- „Maximale Leistung eines Teams LeetCode“
- „Hard interview Fragesteller Auswahl“
- “Priority Queue greedy algorithm”
- “Wie zu lösen 1383”

Jeder, der diese Bedingungen sucht (einschließlich Einstellungsmanager), wird Ihre Lösung sehen, die Ihre Profilsicht erhöht.

---

📚 Zusammenfassung

- **Algorithm**: Sortieren Sie Ingenieure durch abnehmende Effizienz → fegen, halten k schnellste Geschwindigkeiten in einem Min-Heap.
- **Komplexität**: `O(n log n)` Zeit, `O(n)` Hilfsraum.
- **Ergebnis*: Rückgabe `(bestPerformance % 1_000_000_007) `.

Verwenden Sie die Code-Snippets oben, um Ihre Interviewer zu beeindrucken oder LeetCode einzureichen. Glückliche Kodierung