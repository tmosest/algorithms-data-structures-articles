---
Titel: LeetCode 3078. Spiel Alphanumerisch Muster in Matrix Ich...
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
3078. Spiel Alphanumerisch Muster in Matrix I
**Medium************************************************************************************************************************************************************************************************************************************************************

---

### 1. Problem Recap

Sie werden gegeben

* `board`: eine `m × n` Matrix von Ziffern (0‐9).
* `pattern`: eine `p × q` Zeichenmatrix – jedes Zeichen ist entweder eine Ziffer (`'0'`````````9'') oder ein Kleinbuchstaben (`a'````z'````).

Eine Submatrix von `board` **Matches** `pattern` wenn aus jedem einzelnen Buchstaben in `pattern` eine Zuordnung zu einer *einzigen* Ziffer besteht, so dass nach dem Aufbringen der Zuordnung jede Zelle in der Submatrix der entsprechenden Zelle in `pattern` entspricht.
Digits in `pattern` muss genau dem Board entsprechen.

Rückgabe der Koordinaten `[row, col]` der **ober-linken Ecke* der frühesten passenden Sub‐Matrix (unterste Zeile, dann unterste Spalte).
Wenn kein Spiel vorhanden ist, `[-1, -1]` zurückgeben.

---

### 2. Warum dieses Problem eine große Interviewfrage ist

| Gut | Schlecht | Ugly |
|--------------------
| **Conceptual Tiefen** – testet Ihr Verständnis von Musteranpassung, bijizierendem Mapping und 2‐D-Traversal. | **Edge‐case Müdigkeit** – viele Off-by-One-Fehler, insbesondere bei der Mapping von Briefen an Ziffern. | **Time‐Druckfalle** – naive O(m2n2)-Lösungen können bei versteckten immer noch passieren, aber das Risiko „Time‐limit Ã1⁄4bertroffenen Ã1⁄4bertroffen“ hinausgehen. |

- **Good**: Das Problem ist klein genug (≤ 50×50), um Sie brute‐force zu lassen, aber es zwingt Sie, über *bijection* zwischen Buchstaben und Ziffern nachzudenken.
- **Bad**: Es ist einfach, einen korrekten Algorithmus zu schreiben, aber falsche Antworten auf Eckenfälle wie wiederholte Briefe, Digi-Brief-Konflikte oder Muster, die die Board-Grenz berühren.
- **Ugly**: Wenn Sie vergessen, Ihre Mapping zwischen verschiedenen Top-Link-Positionen zurückzusetzen, erhalten Sie falsche Positive.

Vorbereitung für dieses Problem wird Sie komfortabel mit:
* Zweidimensionale Array-Traversal
* Mapping Einschränkungen und Konflikterkennung
* Frühe Ausstiegsbedingungen ( sobald eine Fehlanpassung gefunden wird)

Alle davon sind Heftklammern von hochrangigen Codierung Interviews bei FAANG, Amazon, Google usw.

---

### 3. Lösungsübersicht

ANHANG **Bewertung über alle möglichen Startpositionen* *
Für jeden `r` in `[0, m - p]` und `c` in `[0, n - q]` betrachten wir die Sub‐Links-Ecke, deren obere linke Ecke `(r, c)` ist.

2. ** Zwei Karten halten**
* `digit → Buchstaben` (Array der Größe 10, initialisiert auf `-1`)
* `letter → digit` (array of size 128 or a hashmap)

Diese beiden Karten garantieren den Bijektionsbedarf.

3. **Verwalten der Submatrix**
Für jede Zelle `(i, j)` im Muster:
* Wenn `pattern[i][j]` eine Ziffer ist, muss sie den Board-Wert bei `(r+i, c+j)` gleichstellen.
* Wenn es ein Buchstabe ist:
* Wenn wir diese Board-Nummer bereits abgebildet haben, muss der abgebildete Buchstabe gleich sein.
* Wenn wir diesen Brief bereits abgebildet haben, muss die abgebildete Ziffer gleich sein.
* Wenn keine Kartierung existiert, stellen Sie beide fest.

4. **Die ersten Koordinaten zurücksetzen* *
Da wir zuerst Zeilen iterieren, Spalten zweite, ist das erste erfolgreiche Spiel automatisch das lexikographisch kleinste.

5. **Wenn keine Übereinstimmung besteht, `[-1, -1]` zurückgeben. **

Komplexität:
*Zeit*: `O((m-p+1)(n-q+1) * p * q)` – schlimmster Fall ≈ `503 = 125 000` Operationen.
*Space*: `O(1)` – nur fix-size-Arrays für die beiden Karten.

---

### 4. Referenz-Implementierungen

Hier finden Sie saubere, idiomatische Lösungen in **Java, Python und C++**.
Alle drei folgen der gleichen Logik wie oben beschrieben.

---

(## 4.1 Java

``java
java.util importieren. Strahlen;

Klasse Lösung {
public int[] findPattern(int[][] Board, String[] Pattern) {\cHFFFF}
int m = Board.length, n = Board[0]. Länge
int p = Muster.Länge, q = Muster[0].Länge();

für (int r = 0; r + p <= m; r++) {
für (int c = 0; c + q <= n; c++) {
int[] digitToLetter = new int[10]; // 0 bedeutet unmaped
int[] letterToDigit = new int[128]; // -1 bedeutet nicht
Arrays.fill(digitToLetter, 0);
Arrays.fill(BriefToDigit, -1)

boolean ok = true;
für (in i = 0; i < p & o; i++) {\cHFFFF}
für (int j = 0; j < q & o; j++) {\cHFFFF}
In den Warenkorb Val = Board[r + i][c + j];
char pat = pattern[i].charAt(j);

wenn (Character.isDigit(pat)) {
wenn (pat - '0' !=boardVal) ok = falsch;
} sonst { // Brief
wenn (digitToLetter[boardVal] == 0)
// neue Kartierung
wenn (letterToDigit[pat] == -1)
digitalToLetter[boardVal] = pat;
BriefToDigit[pat] = BoardVal;
} auch
// derselbe Brief auf eine andere Ziffer abgebildet
ok = falsch;
}
} auch wenn (digitToLetter[boardVal] != pat) {
// Board Digit bereits in einem anderen Brief abgebildet
ok = falsch;
}
}
}
}

wenn (ok) neue Int[]{r, c} zurückgeben;
}
}
neue Int[]{-1, -1} zurückgeben;
}
}
`` `

---

4,2 Python

```python
aus der Einfuhr Liste

Klasse Lösung:
def findPattern(self, board: List[List[int]], pattern: List[str]) -> Liste[int]:
m, n = len(board), len(board[0]
p, q = len(pattern), len(pattern[0])

für r im Bereich (m - p + 1):
für c im Bereich (n - q + 1):
# Ziffer -> Buchstabe (0 bedeutet nicht)
d2l = [0] * 10
# Buchstaben -> Ziffer (-1 bedeutet nicht)
L2d = [-1] * 128
ok = Wahr

für i im Bereich(p):
wenn nicht ok:
Bruch
für j im Bereich(q):
num = Board[r + i][c + j]
ch = Muster[i][j]

wenn ch.isdigit():
wenn int(ch) != num:
ok = Falsch
Bruch
andere: # Buchstaben
wenn d2l[num] == 0:
wenn l2d[ord(ch)] == -1:
d2l[num] = ch
l2d[ord(ch)] = num
andere:
ok = Falsch
Bruch
elif d2l[num] ch:
ok = Falsch
Bruch

wenn ok:
zurück [r, c]

zurück [-1, -1]
`` `

---

4,3 C++

```cpp
#include <vector>
#include <string>
mit Namespace std;

Klasse Lösung {
öffentlich:
vektor<int> findPattern(vector<vector<int>>& board, vector<string>& pattern) {\cHFFFF}
int m = Board.size(), n = Board[0].size();
int p = pattern.size(), q = pattern[0].size();

für (int r = 0; r + p <= m; ++r) {\cHFFFF}
für (int c = 0; c + q <= n; ++c) {
int d2l[10] = {0}; // digital -> Buchstabe (0 bedeutet nicht abgebildet)
int l2d[128];
fill(begin(l2d), end(l2d), -1); // letter -> Zahl

bool ok = true;
für (in i = 0; i < p & o; ++i) {\cHFFFF}
für (int j = 0; j < q & o; ++j) {
Int num = Board[r + i][c + j];
n = Muster[i][j];

wenn {\cHFFFF}
wenn (ch - '0' != num) ok = falsch;
} sonst { // Brief
wenn (d2l[num) == 0)
wenn (l2d[(int)ch] == -1)
d2l[num] = ch;
l2d[(int)ch] = num;
} auch
ok = falsch;
}
} auch wenn (d2l[num) != c)
ok = falsch;
}
}
}
}

wenn (ok) wieder {r, c};
}
}
zurück {-1, -1};
}
};
`` `

---

### 5. Testing & Edge Cases

| Test | Grund |
|-------------------
| `board = [[0]]`, `pattern = ["a"]` | Einzelzelle, Brief Mapping. |
| `board = [[5,5],[5,5]]`, `pattern = ["aa","aa"]` | Alle gleichen Ziffern – Mapping muss konsequent sein. |
| `board = [[1,2],[3,4]]`, `pattern = ["a1","2b"]` | Mixed digit/letter mismatch. |
| `board` oder `pattern` an der Grenze | Stellen Sie sicher, dass wir nie aus-of-bounds lesen. |
| `pattern` mit wiederholten Buchstaben mit verschiedenen Ziffern | Sollte scheitern. |

Die vorgesehenen Implementierungen gegen die obigen Fälle (und die Probentests von LeetCode) liefern alle die erwarteten Ergebnisse.

---

### 6. Interview Tipps

ANHANG **Klarieren Sie die Bijektion** – fragen Sie den Interviewer, ob verschiedene Buchstaben auf verschiedene Ziffern abbilden müssen.
2. **Talk durch Ihre Mapping-Arrays** – erklären Sie, warum Sie zwei Karten benötigen und wie Sie Einzigartigkeit durchsetzen.
3. **Diskuss-Komplexität** – weist darauf hin, dass die brute‐force für die Zwänge gut ist, kann aber optimiert werden, wenn das Board groß ist.
4. **Edge‐case thinking** – Erwähnen Sie Off-by-one-Fehler und wie Ihre Schleifen sicherstellen, dass wir im Board bleiben.
5. **Return ordering** – betonen, dass die iterierenden Zeilen zuerst die kleinsten Koordinaten garantieren.

---

### 7. SEO‐Optimierter Takeaway

> Masterstudiengang **LeetCode 2384** (Board Pattern Matching) – eine klassische 2‐D-Musteranpassungs-Herausforderung, die bijektive Kartierungen, zweidimensionale Traversen und frühe Ausstiegsstrategien lehrt. Tauchen Sie in saubere **Java-, Python- und C++-Lösungen*, Test Edge-Fälle und gehen Interviewer durch Ihre Argumentation, diese hochrangige Rolle bei Google, Amazon oder jedem Top-Tech-Unternehmen zu landen.

Glückliche Kodierung und viel Glück in Ihrem nächsten Interview! 🚀

---

*Vorbereitet von [Ihr Name], Senior Software Engineer & Coding Interview Coach. *