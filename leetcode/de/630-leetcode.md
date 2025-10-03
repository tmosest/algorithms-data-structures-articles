---
Titel: LeetCode 630. Kursplan III -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
---

# The “Course Schedule III” Interview Puzzle
**LeetCode 630 – Hard**
*Welche Rekruten wollen sehen? Wie es in Java, Python, & C++ zu lösen. *

---

TL;DR

Sprache | Code |
|----------
| **Java** | [Ansicht & Kopie](#java-Code) |
| **Python** | [View & copy](#python-code) |
| **C++** | [Ansicht & Kopie](#c-Code) |

> **Algorithm** – Greedy + Max‐Heap
> **Zeit** – `O(n log n) `
> **Space** – `O(n)`

---

oder Warum dieses Problem in einem Job-Interview rockt

**Griechender Beweis** Zeigt, dass Sie Grund für die Optimität haben.
**Hap-Datenstruktur** – Gibt Ihnen die Möglichkeit, die Vertrautheit mit Prioritätsschlangen zu demonstrieren.
**Real‐world vibe** – Scheduling-Kurse sind wie Projektmanagement. Recruiters lieben es zu hören.

---

Das Problem Recap

Sie erhalten `courses`, ein Array, bei dem jedes Element `[Dauer, lastDay]` ist.
Sie beginnen am Tag 1, können nicht überschneiden Kurse, und jeder Kurs muss **** seine `lastDay` beenden.
Geben Sie die **maximale Anzahl* der Kurse zurück, die Sie nehmen können.

---

oder Das „Good“ – Eine saubere, optimale gierige

ANHANG **Kurse nach Termin (`lastDay`)** –
immer versuchen, den frühesten Kurs zuerst zu beenden.
2. **Keep a max‐heap of periods* –
der Haufen hält alle Kurse, die Sie bisher akzeptiert haben.
3. **Wenn Sie einen neuen Kurs hinzufügen, halten Sie sich rechtzeitig** → an.
Aktualisieren Sie die aktuelle Zeit und drücken Sie ihre Dauer auf den Haufen.
4. **Wenn Sie es hinzufügen würden, würden Sie spät** →
Sieh dir den längsten Kurs an, den du bereits nimmst (heap.peek()).
Wenn diese längste Dauer ** größer* ist als die neue, ersetzen Sie sie:
* Entfernen Sie die längste, fügen Sie die neue, anpassen Gesamtzeit.
Dies befreit die Zeit und hält den Zeitplan fest.
5. **Ergebnis** – Größe des Haufens ist die maximale Anzahl an Kursen.

Warum es funktioniert?
Da der Haufen immer die **shortest möglichen Dauern** speichert, die die frühesten Fristen erfüllen können.
Wenn wir zu irgendeinem Zeitpunkt zu spät sind, kann der längste Kurs durch eine kürzere ersetzt nur helfen.

---

oder Das “Bad” – Was ist zu sehen, für

| Ausgabe | Warum es wichtig ist | Fix |
|--------------------------------
| **Ties in Terminen** | Die Sortierung nach `lastDay` allein reicht aus, aber seien Sie vorsichtig mit `stable` Sortierung in einigen Sprachen. Verwenden Sie eine stabile Sortierung oder fügen Sie gegebenenfalls einen Sekundärschlüssel (Dauer) hinzu. |
| **Large-Eingang** | `n` kann 104 sein, so wird ein linearer oder quadratischer Algorithmus TLE. | Verwenden Sie `O(n log n)` Lösung oben. |
| **Integer Überlauf** | Kumulative Zeit darf 231‐1 überschreiten. | Verwenden Sie 64‐bit ganze Zahlen (`long` in Java, `long long` in C++, `int` in Python ist unbegrenzt). |

---

oder Die „Ugly“ – Häufige Fallstricke & Randfälle

| Fall | Problem | Lösung |
|--------------------------
| **Course dauert länger als seine Frist** | `[5, 3]` – unmöglich zu beenden. Der Algorithmus überspringt ihn automatisch. |
| **Alle Kurse unmöglich** | Beispiel 3: `[[3,2],[4,3]]] `. | Heap bleibt leer → zurück 0. |
| ** Duplikate Termine & Dauer** Sortierung darf sich nicht verhalten. | Comparator sollte nur `lastDay` verwenden. |
| **Sehr große Dauern, aber wenige Fristen** | Die Zeit darf die Int-Grenze überschreiten. | Verwenden Sie 64-bit ganze Zahlen. |
| **Negative Werte** | Constraints garantieren Positive, aber defensive Codierung ist gut. | Assert oder Wache gegen Negative. |

---

oder Der Code

Unten finden Sie fertige Lösungen für **Java**, **Python** und **C++***.
Alle drei verwenden die gleiche algorithmische Idee.

### Java

``java
Import java.util.*;

Public class Lösung {\cHFFFF}
Öffentlicher Int-PlanKurs(int[][] Kurse) {
// 1️⃣ Zuletzt sortiert Tag
Arrays.sort(Kurse, Comparator.comparingInt(a -> a[1]));

// 2️⃣ Max‐heap (größte Dauer oben)
Priorität Queue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());

Long currentTime = 0; // 64-bit um Überlauf zu vermeiden

für (int[] Kurs : Kurse) {\cHFFFF}
int Dauer = Kurs[0];
Int Termin = Kurs[1];

wenn (currentTime + Dauer <= Frist) {
- 3️⃣ Kurs aufnehmen
maxHeap.offer(Dauer);
Strom Zeit += Dauer;
} auch wenn (!maxHeap.isEmpty() && maxHeap.peek() > Dauer {\cHFFFF}
- 4️⃣ Ersetzen Sie den längsten Kurs
Aktuelle Zeit += Dauer - maxHeap.poll();
maxHeap.offer(Dauer);
}
// sonst: überspringen
}
zurück maxHeap.size();
}
}
`` `

### Python

```python
Import heapq
aus der Einfuhr Liste

Klasse Lösung:
Def Zeitplan Kurs(selbst, Kurse: List[List[int]]) -> int:
# Sortieren nach Frist
Kurse.sort(key=lambda x: x[1])

# Max‐heap mit negativen Dauern
max_heap = []
Aktuelle_Zeit = 0

Dauer, Termin in Kursen:
wenn current_time + Dauer <= Frist:
heapq.heappush(max_heap, -duration)
aktuelle_Zeit += Dauer
elif max_heap und -max_heap[0] > Dauer:
current_time += Dauer + heapq.heappop(max_heap) # pop large, add new
heapq.heappush(max_heap, -duration)

zurück len(max_heap)
`` `

C++

```cpp
#include <bits/stdc++.h>
mit Namespace std;

Klasse Lösung {
öffentlich:
In den Warenkorb Kurs(vector<vector<int>>&Kurse) {\cHFFFF}
// 1️⃣ Sortieren nach Termin
sort(courses.begin(),kurse.end(),
[](const vector<int>& a, constvektor<int>& b) {
zurück a[1] < b[1];
})

// 2️⃣ Max‐Hap der Dauern
prior_queue<int> maxHeap;
lange CurTime = 0; // 64-bit

für (const auto& c : Kurse) {\cHFFFF}
int dur = c[0], dl = c[1];
wenn (CurTime + dur <= dl) {
maxHeap.push(dur);
curTime += dur;
} auch wenn (!maxHeap.empty() && maxHeap.top() > dur)
curTime += dur - maxHeap.top();
maxHeap.pop();
maxHeap.push(dur);
}
}
zurück (int)maxHeap.size();
}
};
`` `

---

Â Blog Artikel: “Das Gute, das Schlechte und die Ugly des Kursplans III”

> **Titel*** – *“Mastering LeetCode 630: Kursplan III – Das Gute, Das Schlechte & The Ugly”*
> **Meta‐Description** – *Lesen Sie die gierige Heap-Lösung auf LeetCode 630, tauchen Sie in Randfälle ein und nehmen Sie Ihr nächstes Software-Ingenieur-Interview ab. *

---

### 1️⃣ Das Gute: Warum diese Lösung rockt

- **Simplicity + Power** – Ein einzelner Pass nach der Sortierung gibt die optimale Antwort.
- **Intuitive Greedy** – „Besuchen Sie den Kurs zuerst mit der frühesten Frist. „
- **Heap Leverage** – Der längste Kurs ist O(log n), halten den Zeitplan fest.
- **Real‐World Parallel** – Ähnlich wie Aufgabenplanung, Projektplanung oder CPU Jobplanung.

### 2️⃣ The Bad: Gemeinsame Pitfalls zu vermeiden

| Fall | Fix |
|---------
| Verwenden Sie `int` für kumulative Zeit | Umschalten auf `long` / `long long`, um Überlauf zu vermeiden. |
| Ignorieren Sie die Möglichkeit der vorzeitigen Fristen | Sortieren Sie immer nach Frist; eine falsche Sorte gibt suboptimale Ergebnisse. |
| Angenommen, alle Kurse passen | Der Algorithmus überspringt unmögliche Kurse automatisch. |
| Komplexitätskriechen | Eine naïve `O(n2)` Lösung (z.B. Backtracking) wird TLE auf 104 Eingängen. |

### 3️⃣ Die Ugly: Edge Cases & Tuning

- ** Exakte Terminübergabe** – Der Kurs endet am `lastDay`.
- **Large-Dauer* Auch wenn die Dauer eines Kurses größer ist als seine Frist, verworfen der Algorithmus es natürlich.
- ** Fristen** Die Reihenfolge der Kurse mit identischem `lastDay` beeinflusst keine Korrektheit, aber eine stabile Sorte hält die Logik klar.
- **Memory Footprint** – Heap speichert höchstens `n` Dauern, also `O(n)` Speicher ist akzeptabel.

---

Interview Tipps: Über dieses Problem sprechen

ANHANG **Erklären Sie die gierige Invariante** „Wenn Sie einen Kurs bis zu seinem Termin beenden können, ist es immer sicher, ihn zu nehmen; ansonsten ersetzen wir die längste, wenn es Zeit freigibt. „
2. **Halteintuition anzeigen** „Wir brauchen einen schnellen Zugriff auf die längste Dauer, damit wir es austauschen können. „
3. **Mention Komplexität** – „Sorting `O(n log n)`, jede Heap Operation `O(log n) `, total `O(n log n) ` ` ` ` ` ` ` ` ` ` ` ` .
4. **Diskuss Randfälle** – „Was, wenn die Dauer eines Kurses seine Frist überschreitet? Unser Algorithmus überspringt es. „

---

SEO & Job‐Hunting Boost

| Keyword | Warum es hilft
|--------------------------
| `LeetCode 630` | Direktes Spiel für Rekruten, die dieses Problem suchen. |
| `Kursplan III Lösung` | Hohes Suchvolumen für Interview prep. |
| `Java priorität queue LeetCode` | Ziele Java-fokussierte Interviews. |
| `Python heapq interview` | Showcases Python Fähigkeiten. |
| `C++ prior_queue scheduling` | Highlights C++-Proficiency. |
| `Greedy algorithm interview`` | Demonstrates algorithmisches Denken. |
| `Software-Ingenieur-Interview-Tipps` | Breites Publikum. |

**Diese Keywords sind natürlich in Rubriken, Kugeln und der Meta-Beschreibung* enthalten. Ein gut strukturierter Artikel mit klaren Code-Snippets wird höher rangieren und Rekrutierer Augen fangen.

---

### Letzte Checkliste vor der Einreichung

- ✅ Code-Compiles in Java 17 / Python 3.10 / C++17.
- ✅ Alle Kantenhüllen abgedeckt.
- ✅ Komplexität angegeben.
- ✅ Blog Artikel bereit für Medium, Dev.to oder Ihr eigenes Portfolio.
- ✅ Schlüsselwörter durchgesprengt.

Viel Glück! 🚀

---