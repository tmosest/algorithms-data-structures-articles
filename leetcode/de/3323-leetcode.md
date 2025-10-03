---
Titel: LeetCode 3323. Minimieren Sie Connected Groups durch Einfügen von Interval -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
# Mastering LeetCode 3323: **Minimize Connected Groups by Inserting Interval**
> *Java | Python | C++ – Eine Sliding‐Window-Lösung, die 1 e5* passiert

---

oder 1. Problemübersicht

Sie erhalten eine Reihe von **intervals** (jeweils `[start, end] `) und eine maximal zulässige Länge `k` für ein *neues* Intervall, das Sie genau einmal einfügen müssen.
Nach dem Einfügen des Intervalls möchten Sie **minimise** die Anzahl der *verbundenen Gruppen* der Intervalle.

Eine *verbundene Gruppe* ist ein maximaler Satz von Intervallen, die zusammen einen kontinuierlichen Bereich ohne Lücken abdecken.
Beispiel:

| Intervalle verbunden? |
|-------------------------
| | `[[1,3],[3,5],[5,6]] | ✅ (covers 1–6) |
| | |[[1,2],[3,4] | ❌ (Gap 2–3) |

**Return** die kleinste mögliche Anzahl angeschlossener Gruppen nach dem Hinzufügen des neuen Intervalls.

> **Beschränkungen*
> * 1 ≤ `Intervals.length` ≤ 105
> * 1 ≤ `start` ≤ `end` ≤ 109
> * 1 ≤ k ≤ 109

---

oder 2. Warum dieses Problem schwer ist

* **Large Input Size** – O(n log n) ist akzeptabel, aber alles Quadratische wird TLE.
* * **Insertion Must Cover Gaps** – Sie können nicht einfach “verbessern” Intervalle; Sie müssen darüber nachdenken, wie das neue Intervall **multiple** Lücken auf einmal überspannen kann.
* ** Schiebefenster auf Gaps** – Der Schlüsseltrick besteht darin, Lücken zwischen zusammengeführten Intervallen als Folge zu behandeln und ein Schiebefenster zu verwenden, um die längste zusammenhängende Folge von Lücken zu finden, die durch ein einziges Intervall von Länge ≤ k abgedeckt werden können.

---

oder 3. Core Insight

ANHANG **Merge die angegebenen Intervalle* Nach dem Zusammenfügen wird jedes aufeinanderfolgende Paar zusammengeführter Intervalle durch ein *Gap* der Länge `gapStartGapEnd` getrennt.
2. **Gaps sind sortiert* Da wir die ursprünglichen Intervalle zunächst sortiert haben, werden die Lücken automatisch in der Reihenfolge ihrer Startpositionen aufsteigen.
3. **Covering ein zusammenhängender Lückenblock* Wenn wir ein Fenster `[l ... r] von Lücken wählen, muss das neue Intervall vom *start* der ersten Lücke bis zum *end* der letzten Lücke überspannen.
*Erforderliche Länge* = `gaps[r].end - Lücken[l].start`.
4. ** Schiebefenster** – Bewegen Sie einen rechten Zeiger, justieren Sie den linken Zeiger, wenn die benötigte Länge `k` überschreitet. Behalten Sie die maximale Anzahl der Lücken (`r-l+1`), die innerhalb der Grenze passen.
5. **Antwort** – Jede Lücke verschmilzt die Gruppenzahl um eins.
[...]
\text{answer} = \text{groups} - \max_{\text{window}\text{gaps} = (\text{gaps} + 1) - \maxCovered = \text{groups} - \maxCovered
\)

---

oder 4. Algorithm Schritte

ANHANG **Kurzintervalle** beim Ansteigen; wenngleich, am Ende absteigend (so können wir leicht zusammenführen).
2. **Merge** überlappende oder berührende Intervalle → `merged`.
3. **Kollect Lücken* zwischen aufeinanderfolgenden `merged` Intervallen → `gaps`.
4. ** Schiebefenster auf Lücken*
* `l = 0`, `maxCovered = 0`
* Für jeden `r` in `[0 ... gaps.size-1] `
* Während `requiredLength > k`, Inkrement `l`.
* Update `maxCovered = max(maxCovered, r-l+1)`.
5. **Return*** `merged.size() - maxCovered.

---

oder 5. Komplexitätsanalyse

Schritt | Zeit | Raum |
|----------------------
| Sortieren | **O(n log n)** | O(1) Hilfsmittel (sortieren an Ort und Stelle) |
| Verschmelzung | **O(n)* | O(1) |
| Gaps | **O(m)*, wobei *m* = merged.size() | O(m) |
| Schiebefenster | **O(m)** | O(1) |
| **Gesamt*** | **O(n log n)****O(n)** (worst‐case for gaps) |

Dies erfüllt die Zwänge bequem.

---

oder 6. Implementierung – Java

``java
Import java.util.*;

Public class Lösung {\cHFFFF}
int minConnectedGroups(int[][] Intervalle, int k) {
wenn (Intervals == null || Intervalle.length == 0) Rückgabe 0;

// 1. Sortieren nach Anfang; tie‐break nach Ende absteigend
Arrays.sort(Intervalle, a, b) ->
wenn (a[0] == b[0]) Integer.compar(b[1], a[1]) zurückgegeben wird;
Rückkehr Integer.compar(a[0], b[0]);
})

// 2. Verschmelzungsintervalle
List<int[]> merge = new ArrayList<>>;
int curStart = Intervalle[0][0];
int curEnd = Intervalle[0][1];
für (in i = 1; i < Intervalle; Länge; i++)
int[] cur = Intervalle[i];
wenn (cur[0] <= curEnd) { // Überlappung oder Berührung
curEnd = Math.max(curEnd, cur[1]);
Andere { // disjoint
zusammengeführt.add(neues Int[]{curStart, curEnd});
curStart = cur[0];
curEnd = cur[1];
}
}
zusammengeführt.add(neues Int[]{curStart, curEnd});

// 3. Lücken zwischen zusammengeführten Intervallen sammeln
int m = merge.size();
(m ==) 1) zurück 1; // nur eine Gruppe, nichts zu überbrücken
List<int[]> gaps = new ArrayList<>>;
für (in i = 0; i < m - 1; i++) {
int end1 = merged.get(i)[1];
int start2 = merged.get(i + 1)[0];
gaps.add(new int[]{end1, start2}); // Lücke: (end1, start2)
}

// 4. Schiebefenster über Lücken
int l = 0, maxCover = 0;
für (int r = 0; r < gaps.size(); r++) {
// benötigte Länge, um Lücken zu decken[l.r]
während (l <= r && gaps.get(r)[1] - gaps.get(l)[0] > k) {\cHFFFF}
L++;
}
maxCovered = Math.max(maxCovered, r - l + 1);
}

// 5. Ergebnis: Gruppen - maxCovered
zurück merged.size() - maxCovered;
}
}
`` `

---

oder 7. Implementierung – Python

```python
aus der Einfuhr Liste

Klasse Lösung:
def minConnectedGroups(self, Intervalle: List[List[int]], k: int) -> int:
Intervalle.sort(key=lambda x: (x[0], -x[1]))

# Merge
zusammengeführt = []
cur_start, cur_end = Intervalle[0]
für s, e in Intervallen[1:]:
wenn s <= cur_end: # Überlappung / Berührung
cur_end = max(cur_end, e)
andere:
merged.append((cur_start, cur_end))
cur_start, cur_end = s, e
merged.append((cur_start, cur_end))

wenn len(gespeichert) == 1:
Rückkehr 1

# Gaps
Lücken = []
für (s1, e1), (s2, e2) in zip(merged, zusammengefasst[1:]):
gaps.append((e1, s2)) # (end_of_first, start_of_second)

# Schiebefenster
I = 0
max_covered = 0
für r in range(len(gaps)):
bei l <= r und Lücken[r][1] - Lücken[l][0] > k:
= 1
max_covered = max(max_covered, r - l + 1)

zurück len(merged) - max_covered
`` `

---

oder 8. Implementierung – C++

```cpp
#include <bits/stdc++.h>
mit Namespace std;

Klasse Lösung {
öffentlich:
int minConnectedGroups(vector<vector< int>& Intervalle, int k) {
sort(intervals.begin(),intervall.end(),
[](const vector<int>& a, constvektor<int>& b) {
wenn (a[0] == b[0]) ein[1] > b[1] zurückgegeben wird;
Rückgabe a[0] < b[0;
})

// Verschmelzungsintervalle
vektor<pairlong lang, lang> zusammengeführt;
langes CurStart = Intervalle[0][0];
langes CurEnd = Intervalle[0][1];
für (size_t i = 1; i < Intervalle.size(); ++i)
lange s = Intervalle[i][0];
lange e = Intervalle[i][1];
wenn (s <= curEnd) { // überlappen
curEnd = max(curEnd, e);
} auch
merge.emplace_back(curStart, curEnd);
curStart = s;
curEnd = e;
}
}
merge.emplace_back(curStart, curEnd);

wenn (merged.size() == 1) Rückgabe 1;

// Gewinne zwischen zusammengeführten Intervallen
vektor<pairlong lang, lang> Lücken;
für (size_t i = 0; i + 1 < merge.size(); ++i)
langes Ende1 = zusammengeführt[i].sekunde;
langes Start2 = zusammengeführt[i + 1].first;
gaps.emplace_back(end1, start2); // (end, start)
}

// Schiebefenster über Lücken
Größe_t l = 0, maxCovered = 0;
für (size_t r = 0; r < gaps.size(); ++r)
während (l <= r && gaps[r].second - gaps[l].first > k) {\cHFFFF}
++l;
}
maxCovered = max(maxCovered, r - l + 1);
}

Rückgabe statische_cast<int>(merged.size() - maxCovered);
}
};
`` `

---

oder 9. Edge Cases Handled

| Edge | Wie wir es handhaben
|---------------------------
| Keine Intervalle | Return 0 (unwahrscheinlich aufgrund von Einschränkungen) |
| Alle Intervalle bereits überschneiden → eine Gruppe | Return 1 sofort |
| Neues Intervall kann keine Lücke | `maxCovered = 0`, Antwort = `groups` abdecken |
| Gaps genau der Länge `k` | Fenster enthält sie (≤ k) |

---

oder 10. Testing – Quick Unit Test (Java)

``java
öffentliche statische Leerstelle (String[] args) {
int[][] a = {1, 3}, {3, 5}, {6, 7}, {8, 9}, {10, 11};
System.out.println(new Solution().minConnectedGroups(a, 4)); // erwartet 2
}
`` `

Führen Sie den gleichen Test auf Python und C++ aus, um die Konsistenz zu bestätigen.

---

11. Take‐Away für Ihr Interview

* ** Denken Sie immer daran, zuerst zu verschmelzen* – Reduziert das Problem auf eine lineare Abfolge von Lücken.
**Treat Lücken als Hauptdatenstruktur** Sie sind die einzigen Teile, die Sie “Brücke” können.
* **Verwenden Sie ein Schiebefenster* Die klassische Zwei-Punkte-Technik gilt auch dann, wenn die Einspannung des Fensters von einem berechneten Unterschied abhängt (`gapEnd - gapStart`).
* **Beware of ganzzahliger Überlauf** – Gaps und benötigte Längen können 109 erreichen, so verwenden Sie 64-Bit-Typen (Java `long`, C++ `long long `, Pythons native ganze Zahlen).

---

oder 12. Weitere Reading & Verwandte Probleme

**“Maximale Anzahl nicht überschneidender Intervalle”** – klassisches Schiebefenster
**“Merge Intervals“* – Grundproblem bei Intervallmanipulation
**“Longest Subarray mit Summe ≤ k”* – Schiebefenster analog für Summen

---

13. Letztes Urteil

Mit der fusion‐gap‐sliding‐window-Strategie wird das Problem nach der Sortierung eine Frage von ** einem linearen Pass**.
Diese elegante Lösung übergeht nicht nur die Zeitgrenzen, sondern gibt Ihnen auch eine saubere, pflegefähige Code-Basis in Java, Python und C++.

> **Happy Codierung!** 🎉

---

> **Keywords**: Intervall-Merging, Lücken, Schiebefenster, LeetCode, Algorithmus-Interview, Zeitkomplexität O(n log n).