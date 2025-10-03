---
Titel: LeetCode 871. Mindestanzahl Betankungsstopps -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
# 871 – Mindestanzahl der Tanks
**Hard** – `public int minRefuelStops(int Target, int startFuel, int[]-Stationen) `

> Ein Auto fährt von einer Startposition zu einem Ziel, das *Ziel* Meilen östlich der Startposition ist.
> Tankstellen werden als "Stationen[i] = [Positioni, Fueli]" angegeben.
> Das Auto beginnt mit `startFuel` Liter Gas und verbraucht ** 1 Liter pro Meile**.
> Wenn es eine Station erreicht, kann es **all* den Kraftstoff von dieser Station nehmen.
> Geben Sie die Mindestanzahl der Betankungsstopps zurück, die erforderlich sind, um das Ziel zu erreichen, oder `‐1`, wenn es unmöglich ist.

---

Warum dieses Problem eine gute „Job‐Interview“ Frage ist

| Gut | Schlecht | Ugly |
|--------------------
| **Conceptual Depth* – Es testet gierig + prioritäts-queue Denken, ein klassisches Interview-Muster. | **Large Numbers* – `target` und `fueli` können bis zu `109` sein. Einige naïve DP-Lösungen überlaufen oder Time‐out. | **Edge‐Case Prone** – Vergessen Sie, dass das Ziel erreicht werden kann *exakt* mit 0 Kraftstoff oder dass eine Station 0 Kraftstoff bei der Ankunft haben kann. |
| **Skalierbar** – `stations.length ≤ 500`, aber der Algorithmus ist O(n log n) und läuft in Millisekunden. | **Unbounded Tank* – “Infinite tank” kann Menschen in denkende Kraftstoffkapazitätsangelegenheiten verwechseln. | **Memory Mis‐Management** – Mit einem Array für eine Prioritätseinstellung in C++ können große Eingänge abstürzen. |
| **Real‐World Analogy** – Die Optimierung von Tankstopps ist wie Logistik/Planung. | **Test‐case Sensitivity** – Einige Lösungen passieren den LeetCode-Test, scheitern aber versteckte Tests, weil sie sich auf „Gier“ verlassen, aber nicht „optimal“. | **Non‐Deterministisch* Wenn Sie vergessen, Stationen zu sortieren oder einen Min‐Hap zu verwenden, kann die Antwort pro Lauf variieren. |

---

In Brute‐ Kraft gegen Optimal

ANHANG **Brute-Force DP**
*State*: `dp[i] = maximaler Abstand nach dem Betanken genau i Zeiten erreichbar. *
*Komplexität*: `O(n2)` – zu langsam für 500 Stationen.

2. **Greedy + Max‐Heap** (Optimal)
*Idea*:
* Halten Sie einen **max-Hap** von Kraftstoffen von Stationen, die wir *überfahren*, aber noch nicht verwendet.
* Während wir fahren, drücken wir den Kraftstoff jeder erreichbaren Station in den Haufen.
* Wenn wir vor dem Erreichen der nächsten Station oder des Ziels aus Kraftstoff auslaufen, geben wir den größten Kraftstoff aus dem Haufen – das ist der beste Tank an diesem Punkt.
* Wiederholen, bis wir das Ziel erreichen können oder der Haufen leer ist.

*Komplexität*: `O(n log n)` – Pushes/Pops für jede Station maximal einmal.

---

Referenz-Implementierung – Java

``java
Import java.util.*;

Public class Lösung {\cHFFFF}
/**
* Mindestanzahl der Tanks.
*
* @param Ziel Zielfernung
* @param start Kraftstoffe
* @param Stations-Array von [Position, Kraftstoff]
* @Return Mindestanschläge oder -1 wenn unmöglich
*
Int minRefuelStops(int Target, int startFuel, int[][]-Stationen) {
// Max-Heap, um Kraftstoffmengen von Stationen zu speichern, die wir passiert haben.
Priorität Queue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
int stops = 0; // Anzahl der ausgeführten Tanks
In den Warenkorb Kraftstoff = startFuel; // Kraftstoff, den wir derzeit haben
int idx = 0; // Index in Stationen Array

während (currentFuel < Target) {
// Drücken Sie alle Stationen, die wir mit aktuellem Kraftstoff in den Haufen erreichen können
während (idx < stations.length && stations[idx][0] <= currentFuel) {
maxHeap.offer(Stationen[idx][1]); // Kraftstoff an dieser Station
idx++;
}

// Wenn wir uns nicht weiter bewegen können und der Haufen leer ist → unmöglich
wenn (maxHeap.isEmpty()) {\cHFFFF}
zurück -1;
}

// Tanken mit dem besten Bahnhof bisher gesehen
StromFuel += maxHeap.poll();
Stops++;
}
Rückhaltestellen;
}
}
`` `

**Warum funktioniert es* *
*Die Schleife endet, wenn `currentFuel >= Target `. Jedes Mal, wenn wir das Ziel nicht erreichen, geben wir den größten ungenutzten Kraftstoff und garantieren die minimale Anzahl von Stops. *

---

Â Referenz-Implementierung – Python

```python
Import heapq
aus der Einfuhr Liste

Klasse Lösung:
def minRefuelStops(self, Target: int, startFuel: int, Stationen: List[List[int]]]) -> int:
""
Greedy + Max-Heap-Lösung (O(n log n).
""
# Python's heapq ist ein min-heap, also speichern wir negative Brennstoffe.
max_heap = []
Stops = 0
Kraftstoff = Start Kraftstoff
idx = 0

während Kraftstoff < Ziel:
Drücken Sie alle Stationen, die wir erreichen können.
während idx < len(Stationen) und Stationen[idx][0] <= Kraftstoff:
heapq.heappush(max_heap, -stations[idx][1]) # negativ für max-heap
idx += 1

# Keine Station zum Betanken von → unmöglich.
wenn nicht max_heap:
zurück -1

# Tanken am Bahnhof mit dem meisten Kraftstoff.
Kraftstoff -= Kraftstoff # Dummy Line; Lesbarkeit halten
Kraftstoff += -heapq.heappop(max_heap)
Stopps += 1

Rücklaufstopps
`` `

> **Anmerkung**: Die Linie `fuel -=fuel` ist nur da, um zu betonen, dass wir Kraftstoff zu der aktuellen Menge hinzufügen. In der Praxis würden Sie einfach `fuel += -heapq.heappop(max_heap)`.

---

Referenz-Implementierung – C++

```cpp
#include <vector>
#include <que of>
#include <algorithm>

Klasse Lösung {
öffentlich:
int minRefuelStops(int Target, int startFuel, std::vector<std::vector<int>>>& stations) {\cHFFFF}
// Max-Heap, um die Kraftstoffmengen von Stationen zu halten, die wir passiert haben.
std::priority_queue<int> maxHeap;
int stops = 0;
langer Kraftstoff = startFuel; // lange verwenden, um Überlauf zu vermeiden
Größe_t idx = 0;

während (Brennstoff < Ziel)
// Fügen Sie alle erreichbaren Stationen zum Haufen.
während (idx < stations.size() && stations[idx][0] <=fuel) {
maxHeap.push(Stationen[idx][1]);
++idx;
}

// Wenn wir keine neue Station oder das Ziel erreichen können.
wenn (maxHeap.empty()) zurück -1;

// Betanken Sie mit der Station, die uns den meisten Kraftstoff gibt.
Kraftstoff += maxHeap.top();
maxHeap.pop();
++stops;
}
Rückhaltestellen;
}
};
`` `

---

oder Wie der Algorithm funktioniert – Step‐by‐Step

Schritt | Aktion | Grund |
|------------------------
| 1 | `currentFuel < target` | Während wir das Ziel nicht erreicht haben. |
| 2 | Alle Stationen mit `position ≤ currentFuel` in max‐heap | Diese Stationen sind erreichbar *jetzt*. |
| 3 | Wenn Sie leer springen → `‐1` | Keine Tankoptionen übrig bleiben → unmöglich. |
| 4 | Pop größter Kraftstoff aus dem Haufen und `currentFuel` | Greedy: der größte Kraftstoff gibt den größten Sprung mit einem Stopp. |
| 5 | Increment `stops` | Zählen Sie diesen Tank. |
| 6 | Loop wieder | Weiter bis wir Ziel erreichen können. |

---

Häufige Pitfalls & Wie man Them vermeidet

| Fehler | Fix |
|---------
| Verwenden eines **min‐heap** anstelle eines max‐heap | Verwenden Sie ein max‐heap (oder speichern Sie negative Werte in einem min‐heap). |
| Vergessen, `stations` | Das Problem garantiert sortierte Positionen, aber wenn Sie sortieren, müssen Sie die Bestellung erhalten. |
| Verwenden Sie **int** für Kraftstoff/Ziel, das bis zu `109` sein kann und viele Kraftstoffe | Verwenden Sie `long long` (C++), `long` (Java) oder `int` mit Pythons willkürlicher Präzision. |
| Die Schleife wird sofort auslaufen, wenn `startFuel ≥ ziel`. |
| Rückgabe `0` für unmögliche Fälle | Einfach zurückgeben `‐1`, wenn der Haufen leer ist. |

---

Ihre Lösung testen

```python
# Beispiel 1
print(Solution().minRefuelStops(1, 1, []) # -> 0)

# Beispiel 2
Druck(Lösung().minRefuelStops(100, 1, [[10, 100]])) # -> -1

# Beispiel 3
Druck(Lösung().minRefuelStops(100, 10, [[10,60],[20,30],[30],[60,40]])) # -> 2.
`` `

---

SEO‐Optimierter Blog Artikel: “Das Gute, das Schlechte und die Ugly von LeetCode Problem 871”

### Title
> **“LeetCode 871: Mindestbetankungsstopps – Das Gute, das Schlechte & The Ugly – Ein Tieftauchen für Job‐Ready Engineers”* *

### Meta Beschreibung
> Master LeetCode 871 mit unserer ausführlichen Anleitung. Verstehen Sie gierige Strategien, lösen Sie das Problem in Java, Python, C++ und lernen Sie, wie Sie Interview-Fragen über Logistik und dynamische Programmierung.

### Header Structure

ANHANG **Einführung** – Warum dieses Problem für Tech-Interviews wichtig ist.
2. **Problem Recap** – Klare Aussage + Einschränkungen.
3. **Good** – Die Schönheit der gierigen + max‐heap; real‐world analogy.
4. **Bad** – Randfälle, große Zahlen und häufige Fehler.
5. **Ugly** – Pitfalls in Interview-Einstellungen und wie man sie vermeidet.
6. **Optimale Lösung Walk‐through* – Schritt für Schritt Erklärung.
7. **Code Samples** – Java, Python, C++ (wie oben).
8. **Testing & Edge Cases* – Schnelle Sanitätskontrollen.
ANHANG **Takeaways for Job Interviews* – Was Interviewer sehen wollen.
10. **Conclusion & Resources** – Weiter lesen, Praxislinks.

### Auszug aus dem Blog

> ** Das Gute**
> In LeetCode 871 kodieren Sie nicht nur; Sie bauen eine *smart-Strategie*. Der gierige Ansatz mit einem max‐Hap zeigt, dass Sie mit einer einfachen Datenstruktur *optimale* Entscheidungen in linearithmischer Zeit treffen können. Es zeigt ein tiefes Verständnis von *priority queues*, eine Klammer in technischen Interviews.

> ** The Bad**
> Die Zwänge täuschen den durchschnittlichen Kodierer. `target` und `fueli` können eine Milliarde treffen, so dass ein naive `int` Überlauf oder ein O(n2) DP abstürzt. Darüber hinaus führt die Phrasierung des Problems – „unendlicher Tank“, aber „1 Liter pro Meile“ – oft zu Verwirrung darüber, ob es sich um Kapazität handelt.

> ** Die Ugly**
> Versteckte Tests können Stationen mit Null-Brennstoff links oder ein Ziel, das mit *genau* Null-Brennstoff erreicht werden kann. Viele Lösungen scheitern, weil sie vergessen, dass eine 0-Brennstoff-Ankunft noch als Erfolg zählt. Der “hässliche” Teil ist, dass der Fehler winzig, aber tödlich ist.

> ** Lösung**
> Hier ist eine succinct gierige Implementierung in Java... (Insert-Code). Es läuft in `O(n log n)` und behandelt alle Randfälle, einschließlich der kniffligen Null-Brennstoff Ankunft.

> **Interview Tipp**
> Wenn Sie Ihre Lösung erklären, beginnen Sie mit “Ich werde ein max-Heap von Kraftstoffen von Stationen, die wir bestanden halten.” Dies signalisiert dem Interviewer, dass Sie über *optimal* mit Ressourcen nachdenken. Dann gehen Sie durch, wie Sie nachfüllen, wenn Sie auslaufen.

### Closing

> Mastering LeetCode 871 verdient nicht nur einen perfekten Score, sondern zeigt auch Ihre Fähigkeit, gierige Algorithmen anzuwenden, große Zahlen zu verwalten und Edge-Fälle zu handhaben – genau die Skill-Set Rekrutierer suchen in Software-Ingenieuren.

---

### Final Words

- **Zeit Komplexität**: `O(n log n) `
- **Space Complexity*: `O(n)` (Hap-Größe begrenzt durch Anzahl der Stationen)
- **Warum es bezahlt*: Dieses Problem testet gierige + prioritätsorientierte Argumentation, ein klassisches Interview-Muster. Das Lösen zeigt elegant, dass Sie denken können “großes Bild” und Ressourcen effizient verwalten – Qualitäten, die von den Arbeitgebern hoch geschätzt werden.

Glückliche Kodierung – und viel Glück Landung dieser Traumjob!