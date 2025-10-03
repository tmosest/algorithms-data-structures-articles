---
Titel: LeetCode 3128. Rechte Dreiecke - Ja.
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
oder 1. Dreisprachige Lösungen für LeetCode 3128 – *Rechte Dreiecke*

Im Folgenden sind saubere, produktionsfertige Implementierungen in **Java*, **Python** und **C++**, die das Problem in *O(m × n)* Zeit und *O(m + n)* zusätzlichem Speicher lösen, wobei *m* die Anzahl der Zeilen und *n* die Anzahl der Spalten ist.

> **Problem recap**
> Ein **rechtes Dreieck** wird durch drei Zellen gebildet, die alle `1` enthalten.
> Ein Scheitel muss einen **row** mit dem zweiten Scheitel teilen, und der erste Scheitel muss eine **column** mit dem dritten Scheitel teilen.
> Zählen Sie alle diese Dreiecke in einer binären Matrix.

---

### 1.1 Java

``java
Import java.util.*;

Klasse Lösung {
Public long numberOfRightTriangles(int[][]raster) {
int Zeilen = Raster.Länge;
int cols = Raster[0]. Länge

// Zählen Sie in jeder Zeile und Spalte
int[] ZeileCnt = neu int[rows];
int[] colCnt = new int[cols];

für (int r = 0; r < Zeilen; r++) {
für (int c = 0; c < cols; c++) {\cHFFFF}
wenn (grid[r][c] == 1) {
Zeile Cnt[r]++;
ColCnt[c]++;
}
}
}

lange Dreiecke = 0;
für (int r = 0; r < Zeilen; r++) {
für (int c = 0; c < cols; c++) {\cHFFFF}
wenn (grid[r][c] == 1) {
// (rowCnt[r] - 1) Optionen für das horizontale Bein
// (colCnt[c] - 1) Auswahlmöglichkeiten für das vertikale Bein
Dreiecke += 1L * (rowCnt[r] - 1) * (colCnt[c] - 1);
}
}
}
Dreiecke zurückgeben;
}
}
`` `

*Warum 'long'? *
Die maximale Anzahl von Dreiecken kann `1012` erreichen (1 000 × 1 000 Raster mit einem gefüllt). `int` würde überlaufen.

---

### 1.2 Python

```python
Klasse Lösung:
Def Nummer OfRightTriangles(self, grid: List[List[int]]) -> int:
Zeilen, cols = len(grid), len(grid[0])

# Zeilen- und Spaltenzähler
Zeile_cnt = [0] * Zeilen
(c) = [0]

für r in range(rows):
für c im Bereich(cols):
wenn Raster[r][c]:
Zeile_cnt[r] += 1
(c) += 1

Dreiecke = 0
für r in range(rows):
für c im Bereich(cols):
wenn Raster[r][c]:
Dreiecke += (row_cnt[r] - 1) * (col_cnt[c] - 1)

zurück Dreiecke
`` `

Pythons willkürlich-präzise Zahlen bedeuten, dass wir uns nicht um Überlauf sorgen müssen.

---

### 1.3 C++

```cpp
#include <vector>

Klasse Lösung {
öffentlich:
Lang lange NummerOfRightTriangles(std::vector<std::vector<int>>>>& grid) {
int Zeilen = grid.size();
int cols = grid[0].size();

std::vector<int> lineCnt(rows, 0), colCnt(cols, 0);

// Anzahl 1 in jeder Zeile und Spalte
für (int r = 0; r < Zeilen; ++r)
für (int c = 0; c < cols; ++c)
wenn (grid[r][c) {\cHFFFF}
++rowCnt[r];
++Cnt[c];
}

lange Dreiecke = 0;
für (int r = 0; r < Zeilen; ++r)
für (int c = 0; c < cols; ++c)
wenn (grid[r][c) {\cHFFFF}
Dreiecke += 1LL * (rowCnt[r] - 1) * (colCnt[c] - 1);
}

Dreiecke zurückgeben;
}
};
`` `

`long long` garantiert sichere 64-Bit-Arithmetik.

---

oder 2. Blog Artikel: “Das Gute, das Schlechte und die Ugly des Gegen rechte Dreiecke”

### 2.1 Warum dieses Problem in Interviews

- **Matrix-Traversal** – eine Reihe von Interviewfragen.
- **Kombinationszählung* – testet, ob Sie *O(m × n)* Lösungen anstelle von brute‐force O((m × n)3) erkennen können.
- **Edge‐case Thinking** – Umgang mit sehr großen Ausgängen und Speicherzwängen.
- **Cross-language fluency** – Interviewer fragen oft nach Java/Python/C++ Lösungen auf der Fliege.

### 2.2 Das Gute – Intuition & Einfachheit

Die wichtigsten Erkenntnisse:
> *Wenn eine Zelle (r, c) ein rechtwinkliger Scheitel ist, kann jeder andere `1` in seiner Reihe das horizontale Bein sein, und jeder andere `1` in seiner Spalte kann das vertikale Bein sein. *

So brauchen wir für jeden `1` nur die Zählungen von `1`s in seiner Zeile und Spalte.
Die Anzahl der Dreiecke mit dieser Zelle als rechter Winkel ist einfach
`(rowCount[r] – 1) × (colCount[c] – 1) `.

Dies reduziert eine scheinbar kombinatorische Explosion zu einem Linearpass.

### 2.3 The Bad – Naïve wendet sich an TLE

A Straightforward O((m × n)3) Algorithmus würde:
ANHANG Zählen Sie alle Dreier von Zellen.
2. Überprüfen Sie den geometrischen Zustand.

Auch für ein 100x100-Gitter handelt es sich dabei um Milliarden von Operationen – weit über die Zeitgrenzen hinaus.
Die Zwänge des Problems (1000 x 1000) regeln jede kubische oder quadratic‐in‐cells-Lösung.

### 2.4 The Ugly – Corner Cases & Overflow

- **Alle Zellen sind `1`*:
Die Anzahl der Dreiecke kann so hoch sein wie
`Σ (rowCount[r] – 1) × (colCount[c] – 1) ≈ `1012`.
Mit einem 32-Bit-Integer-Überlauf; Verwenden Sie 64-Bit (`long`/`long long``).
- **Sparse Grids*:
Viele Zeilen/Spalten enthalten Null `1`s. Unser Algorithmus behandelt dies anmutig, weil `(rowCount[r] – 1)` nur dann negativ wird, wenn `rowCount[r] == 0`, aber wir bewachen, indem wir `grid[r][c] == 1` vor der Berechnung des Produkts.
- **Non‐rectangular Inputs*:
LeetCode garantiert `grid[i].length` ist konstant, aber defensive Code kann jagged Arrays behaupten oder handhaben.

### 2.5 Step‐by‐Step Walkthrough (Java)

```text
ANHANG Zählen Sie 1 in jeder Zeile → ZeileCnt[]
2. Zähler 1s in jeder Spalte → colCnt[]
3. Für jede Zelle, die 1:
Dreiecke += (rowCnt[r] - 1) * (colCnt[c] - 1)
`` `

Die ersten beiden Pässe sind O(m × n).
Der dritte Pass ist auch O(m × n).
Gesamtzeit: **O(m × n)**.
Extraspeicher: **O(m + n)** für die Zähler.

### 2.6 Komplexitätsanalyse

| Operation | Zeit | Raum |
|---------------------
| Zählreihen | O(m × n) | O(m) |
| Zählspalten | O(m × n) | O(n) |
| Dreiecke | O(m × n) | O(1) (außer Zählern) |
| **Gesamt*** **O(m × n)****O(m + n)**

Dies erfüllt die Zwänge bequem:
- Für ein 1000 × 1000 Raster: ~ 1 000 000 Operationen, ~8 KB Hilfsspeicher.

### 2.7 Testen & Edge‐ Fallprüfung

| Test | Grid | Erwartet | Grund |
------------------------------------
| Alle Nullen | 3×3 alle `0` | 0 | Keine Dreiecke |
| Alle | 4×4 alle `1` | 4 * (3 * 3) = 36 | Max zählt |
| Sparse ones | 3×3 mit isoliert `1` | 0 | Benötigen Sie mindestens zwei 1s in derselben Zeile / Spalte |
| Non‐square | 2×5 Raster | Zählen Sie entsprechend | Zeigt rechteckige Formen |
| Großer Eingang | 1000x1000 mit 50% | Laufen in <0.1 s | Performance Benchmark |

### 2.8 Take-aways für Ihr nächstes Interview

- **Start mit Zählhilfen*: Wenn ein Problem "gleiche Zeile / gleiche Spalte" Zwänge, vorkompute Zeile / Spalte Frequenzen.
- **Behüte dich bei ganzzahligem Überlauf**: Wenn Sie vermuten, dass die Ergebnisse 231 – 1 überschreiten können, verwenden Sie 64-Bit-Typen.
- **Erklären Sie Ihre Logik*: Auch wenn Ihr Code perfekt ist und die Intuition (wie die „Rechtwinkel-Scheibe“-Ansicht) artikuliert, beeindruckt Interviewer.
- ** Zeit-Komplexität zuerst*: Zeige dir O((m × n)3) an und warum es vor der Präsentation der O(m × n)-Lösung ausfällt.

### 2.9 Letztes Urteil

- **Good** – Ein schöner *O(m × n)* Algorithmus, der sowohl **effizient** als auch ** lesbar** ist.
- **Bad** – Jeder brute‐force-Ansatz wird *time‐out* auf großen Testfällen.
- **Ugly** – Achten Sie auf Überlauf und Sparsamkeit, aber ein sorgfältiges 64-Bit-Produkt repariert es.

Dieses Problem ist ein *klassisches Beispiel*, wie eine einfache kombinatorische Beobachtung eine scheinbar annehmbare Herausforderung in eine saubere, interviewfreundliche Lösung verwandeln kann. Mastering wird Ihnen eine solide Grundlage für jede matrixbasierte Interviewfrage geben.

---

### 2.9 Möchten Sie noch mehr beeindrucken?

- ** Einen Ein-Liner für Python** hinzufügen:
```python
Dreiecke = Summe((row_cnt[r]-1)*(col_cnt[c]-1)
für r in range(rows) für c in range(cols) wenn grid[r][c])
`` `
- **Diskussparallelisierung*: Zwei separate Scans können parallel durchgeführt werden; sprechen Sie über die Möglichkeit, wenn der Interviewer über *distributed Computing* fragt.

### 2.10 Schlussworte

Das Zählen der rechten Dreiecke ist ein Mikrokosmos des *“Matrix + Combinatorik + sorgfältiges Zählen”* Interview Thema. Durch das Erlernen des Musters der „Rechtwinkel-Vertex“-Zählung sind Sie bereit für eine Vielzahl von Interview-Fragen, die Sie an *count*-Strukturen innerhalb von 2-D-Gittern stellen.

Glückliche Kodierung – und viel Glück bei Ihrem nächsten Interview!