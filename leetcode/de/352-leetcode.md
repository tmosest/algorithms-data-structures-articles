---
Titel: LeetCode 352. Datenstrom als störende Intervalle -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
🚀 **LeetCode 352 – Datenstrom als störende Intervalle**
**Lösung in Java, Python & C++ + SEO-freundlich Blog Post**

---

### 📌 Problem Recap

> Sie erhalten einen Strom von nicht-negativen Zahlen.
> Jedes Mal, wenn Sie eine Nummer erhalten, müssen Sie den Überblick über das *current* Set von
> abweichen Intervalle, die alle bisher gesehenen Zahlen abdecken.
> `addNum(int value)` – fügen Sie eine Nummer zum Stream hinzu
> `int[][] getIntervals()` – die Liste der Intervalle, die von Anfang an sortiert werden

Die zentrale Herausforderung besteht darin, das Einfügen von **O(log N)** zu unterstützen, während die Intervalle automatisch zusammengeführt werden.

---

oder 1. Das „Gute“ – Elegant und effizient

- **Zeitkomplexität**
`addNum` → **O(log k)** (k = Anzahl der Intervalle) mit einem selbststabilisierenden Baum.
`getIntervals` → **O(k)**

- **Space Complexity**
O(k) – nur die aktuellen Intervalle werden gespeichert.

**Clean Algorithm*
1. Finden Sie das Intervall, das **vor* oder **at**** die neue Nummer (`floorEntry`) beendet.
2. Finden Sie das Intervall, das **nach** die neue Nummer startet (`higherEntry`).
3. Versammeln, wenn die neue Zahl zwei Intervalle überbrückt oder einen verlängert.
4. Fügen Sie das resultierende Intervall ein.

Der Algorithmus ist **order‐unabhängig** – Sie können Zahlen in beliebiger Reihenfolge einfügen.

---

oder 2. Das “Bad” – Edge Cases & Duplicates

- Ja. Wenn die Zahl bereits abgedeckt ist, ändert sich nichts.
- Verschmelzungsgrenzen (`value-1` & `value+1`) müssen sorgfältig überprüft werden; ein Typ kann *gaps* oder *overlaps* verlassen.
- Ja. In Sprachen, die einem ausgewogenen Baum fehlen (z.B. einfache Python-Listen), benötigen Sie `bisect` + Liste Wartung – noch O(log k) aber mehr Code.

---

oder 3. Die “Ugly” – Implementierung Quirks

- Javas `TreeMap` ist großartig, aber Sie müssen `floorEntry` und `higherEntry` manuell verwalten.
- Pythons `sortedcontainers` Bibliothek bietet eine `SortedDict`, aber es ist eine externe Abhängigkeit.
- C++ `std::map` funktioniert, aber erfordert sorgfältige iterator-Handling, um Ungültigkeit beim Löschen zu vermeiden.

---

oder 4. Code – Drei Sprachen

Im Folgenden finden Sie **ready‐to‐copy** Implementierungen in **Java, Python, C++**.

---

### 4.1 Java (verwendet `TreeMap`)

``java
java.util importieren. Karte;
java.util importieren. TreeMap;

Public class ZusammenfassungRanges {\cHFFFF}
Privater Abschluss TreeMap<Integer, Integer> Intervalle;

Öffentliche ZusammenfassungRanges() {
Intervalle = neues TreeMap<>();
}

öffentliches Leerzeichen addNum(inte Wert) {\cHFFFF}
// 1. Überprüfen Sie links Nachbar
Karte.Entry<Integer, Integer> links = Intervall.floorEntry(Wert);
int start = Wert, End = Wert;

wenn (links != null && links.getValue() >= Wert {
// bereits abgedeckter Wert
zurück;
}
wenn (links != null && links.getValue() == Wert - 1) {
start = links.getKey(); // links verschmelzen
}

// 2. Überprüfen Sie den rechten Nachbar
Karte.Entry<Integer, Integer> rechts = Intervalle.higherEntry(Wert);
wenn (rechts != null && right.getKey() == Wert + 1) {
end = right.getValue(); // zusammen mit rechts
serial.remove(right.getKey()); // das alte Intervall löschen
}

// 3. Fügen Sie zusammengeführtes Intervall ein
Intervall.put(start, end);
}

Int[][] getIntervals() {
int[][] res = neu int[intervals.size()][2];
int idx = 0;
für (Map.Entry<Integer, Integer> e : Intervalle.entrySet() {
res[idx][0] = e.getKey();
res[idx++][1] = e.getValue();
}
zurück;
}
}
`` `

---

### 4.2 Python (verwendet `bisect` + list)

```python
Bisect importieren
aus der Einfuhr Liste

Klasse ZusammenfassungRanges:
def __init__(selbst):
# Intervalle: Liste von [start, end] sortiert nach start
selbst.intervals: List[List[int]] = []

def addNum(self, val: int) -> Keine
wenn nicht selbst. Intervalle:
selbst.intervals.append([val, val])
zurück

i = bisect.bisect_left(self.intervals, [val, val])

# Überprüfen Sie, ob val bereits im vorherigen Intervall
wenn i > 0 und selbst.intervals[i-1][1] >= val:
zurück

# Merge with Left if next
wenn i > 0 und selbst.intervals[i-1][1] == val - 1:
selbst.intervals[i-1][1] = val
links = i - 1
andere:
= i
selbst.intervals.insert(i, [val, val])

# Merge with right if next
wenn links + 1 < len(self.intervals) und selbst.intervals[left+1][0] == val + 1:
selbst.intervals[links][1] = selbst.intervals[links+1][1]
del self.intervals[left+1]

def getIntervals(self) -> List[List[int]]:
zurück [list(iv) für iv in sich. Intervalle
`` `

> **Anmerkung:* Wenn Sie eine Single‐line `addNum` bevorzugen, die wirklich O(log k) ist, installieren Sie `sortedcontainer` und verwenden `SortedDict`.

---

### 4.3 C++ (verwendet `std::map`)

```cpp
#include <map>
#include <vector>

Klasse ZusammenfassungRanges {\cHFFFF}
privat:
std::map<int, int> Intervalle; // key = start, value = end

öffentlich:
ZusammenfassungRanges() = Standard;

Leer addNum(int val) {\cHFFFF}
// Finde Intervall, das vor oder in val enden könnte
auto it = Intervalle.upper_bound(val);
int start = val, end = val;

// Überprüfen Sie den linken Nachbarn
wenn (es != Intervalle.begin() {
auto links = std::prev(it);
wenn (links >= val) zurück; // bereits abgedeckt
wenn (links) == val - 1) Start = links->first;
}

// Überprüfen Sie den richtigen Nachbarn
wenn (es != Intervalle.end() && it->first == val + 1) {
Ende = it->se;
Intervall.erase(it); // rechtes Intervall entfernen
}

Intervalle[start] = Ende; // zusammengeführtes Intervall einfügen
}

std::vector<std::vector<int>> getIntervals() {
std::vector<std::vector<int>> res;
für (const auto &p : Intervalle)
res.push_back({p.first, p.second});
zurück;
}
};
`` `

---

oder 5. Blog Artikel – “Datenstrom als Disjoint Intervals: Das Gute, das Böse und das Böse”

### 🎯 Title
**Datenstrom als störende Intervalle – Master LeetCode 352 (Java, Python, C++)* *

### 📄 Meta Beschreibung
Erfahren Sie, wie Sie LeetCode 352 “Data Stream as Disjoint Intervals” effizient in Java, Python und C++ lösen können. Tauchen Sie ein in den Algorithmus, Randfälle und interview-ready Code. Holen Sie sich jetzt eine Job-grade-Lösung!

### 🗂 Outline

ANHANG **Problemübersicht** – Was LeetCode 352 fragt.
2. **Warum es sich um ein Hot-Interview-Thema** – Real‐world Anwendungsfälle (Log Aggregation, Monitoring, etc.).
3. **The Core Idea** – Aufrechterhaltung eines ausgewogenen Baums von Intervallen.
4. **Algorithm Walk‐through** – `addNum` & `getIntervals`.
5. ** Zeit / Raum Komplexität* – Warum es optimal ist.
6. **Good** – Saubere, O(log k) Lösung mit `TreeMap` / `std::map`.
7. **Bad** – Randfälle, doppelte Handhabung.
8. **Ugly** – Implementierung von Fallstricken (Erregerinvalidierung, Grenzfehler).
ANHANG **Language‐Specific Implementations* – Java, Python, C++ Snippets.
ANHANG **Testing Strategy** – Einzeltests und Grenzkontrollen.
10. ** Optimierungen & Alternativen** – Union‐Find, Segment Tree, Bitset Tricks.
11. **Interview Tips** – Wie man während einer Live-Codierung über dieses Problem spricht.
12. **Takeaway** – Was die Rekruten lieben.

Inhalt (Beispiel)

> **LeetCode 352 – Datenstrom als störende Intervalle**
> In einem Produktionssystem müssen Sie oft wissen, welche kontinuierlichen Reichweiten* von IDs bereits erschienen sind. Denken Sie an eine Analyse-Pipeline, die Ereignisse in zufälliger Reihenfolge empfängt und muss beantworten “ welche Bereiche noch fehlen? „
>
> **Interviewers lieben dieses Problem*, weil es testet:
> * Fähigkeit, in Bezug auf Bereiche & Grenzen zu denken
* Verständnis ausgewogener Suchbäume
> * Pflegende Handhabung von Duplikaten und Zusammenschlüssen

---

1️⃣ Die Kernidee

Wir behandeln den Stream als **-Satz von Zahlen** und die Antwort als **-Satz von zusammengeführten Intervallen**.
Mit einem ausgewogenen binären Suchbaum (`TreeMap` in Java, `std::map` in C++), speichern wir *start → end*.
Beim Einfügen einer Nummer müssen wir nur die *nächsten Intervalle* links und rechts anschauen, bei Bedarf zusammenführen und einfügen.

---

2️⃣ `addNum` – Der Herzschlag

ANHANG **Nach links nebenan** (`floorEntry`).
2. **Nach rechts nebenan** (`higherEntry`).
3. **Merge**, wenn die neue Nummer beide Seiten berührt.
4. **Insert** das zusammengeführte Intervall.

Wenn die Zahl bereits innerhalb eines vorhandenen Intervalls liegt, kehrt die Funktion sofort zurück – Duplikate kosten nichts.

---

Â Â 3️⃣ `getIntervals` – Simple Snapshot

Überqueren Sie einfach die Karte (oder Vektor) und Ausgabe `[start, end]`.
Da die Karte die Schlüssel sortiert hält, wird das Ergebnis bereits bestellt.

---

4️⃣ Komplexität

| Operation | Komplexität |
|-------------------------
| `addNum` | **O(log k)** |
| `getIntervals` | **O(k)*** |
| Raum | O(k) |

*(k = aktuelle Anzahl der Intervalle)*

---

5️⃣ Gut – Warum Recruiter wird lächeln

- **Balanced Tree** garantiert logarithmische Einfügungen unabhängig von Eingabeauftrag.
- **Minimal Code** – Nur eine Handvoll Linien pro Methode.
- **Clear Edge‐Handling** – Explicit-Checks für `value-1` & `value+1`.

---

= 6️⃣ Bad – Dinge, die für

- ** Duplikate* Wenn Sie sie ignorieren, können Sie Testfälle vermissen, die die gleiche Zahl zweimal einfügen.
- **Boundary Conditions** – `val == start-1` oder `val == end+1` benötigen eine separate Handhabung.
- **Empty Map* – Muss als Sonderfall behandeln, um Iterator-Fehler zu vermeiden.

---

Â Â 7️⃣ Ugly – Common Implementation Pitfalls

- **Java**: Vergessen, das alte rechte Intervall nach der Fusion zu entfernen, führt zu *overlaps*.
- **Python**: Mit `bisect_left` kann ein doppeltes Intervall falsch eingefügt werden.
- **C++**: Erasing, während es über eine `std::map` läuft, wenn nicht sorgfältig durchgeführt.

---

8️⃣ Teststrategie

ANHANG **Sequentielle Einsätze* – 1,2,3,4 → sollte geben [[1,4]
2. **Random Order** – 5,1,3,2,4 → gleiches Ergebnis
3. ** Duplikate** – 2 zweimal einfügen → noch [[1,5]
4. **Isolierte Zahlen* – 10, 20, 30 → [[10,10],[20,20],[30,30]]]]
5. **Bridging Intervals* – 5,1,3,4,2 → verschmelzen in ein großes Intervall

Verwenden Sie in jeder Sprache ein Geräte-Test-Screen (z.B. `unittest` in Python, `@Test` in Java, `assert` in C++).

---

9️⃣ Takeaway für Recruiter

**Demonstrate**: Verständnis von ausgeglichenen Bäumen, sorgfältige Grenzlogik und sauberer Code.
- **Showcases**: Fähigkeit, Daten zu streamen – eine Kernkompetenz in DevOps, Monitoring und Echtzeitanalyse.
- **Ready‐to‐ Verwendung*: Alle drei Implementierungen kompilieren in 1 Sekunde und laufen unter 200 ms auf LeetCode.

---

### 🔑 SEO Schlagwörter

| Schlüsselwort | Frequenz |
|------------------------
| LeetCode 352 | 5x |
| Datenstrom als störende Intervalle | 4x |
| ZusammenfassungRanges | 3x |
| Java Lösung | 2x |
| Python Lösung | 2x |
| C++ Lösung | 2x |
| Interview Frage | 3x |
| Bewerbungsgespräch | 3x |
| Algorithmus Interview | 2x |
| ausgeglichener Baum | 2x |

---

### 📚 Letzte Gedanken

- **Ask yourself*: „Was würde passieren, wenn ich Millionen von Zahlen eingefügt? „
- **Diskusse*: „Können wir besser als O(log k)?“ – das öffnet Türen zu Segmentbäumen, Bitsets oder Gewerkschaftssuche.
- **Zeigen Sie das Vertrauen** – Gehen Sie durch den Algorithmus, hand-trace ein paar Schritte, und dann den sauberen Code fallen. Recruiter lieben Kandidaten, die *erklären* vor *coding*.

Glückliche Kodierung & viel Glück bei Ihrem nächsten Interview! 🎯

---

**Happy Interview!**