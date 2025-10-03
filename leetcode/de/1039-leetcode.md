---
Titel: LeetCode 1039. Mindestpunkt-Triangulation von Polygon -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
📌 LeetCode 1039 – Mindestpunkt-Triangulation von Polygon
*Medium* | * Dynamische Programmierung* | *Matrix‐Chain Multiplikation Variante*

---

### TL;DR
- **Goal** – Ein konvexes Polygon in `n‐2`-Dreiecke so teilen, dass die Summe aus
`value[i] * Wert[j] * Wert[k]` für jedes Dreieck ist minimal.
- **Solution** – Classic **interval DP** (eine Variation der Matrix‐Chain Multiplikation).
- **Komplexe** – `O(n3)` Zeit, `O(n2)` Raum.

---

🔍 Problem Recap

Sie erhalten ein Array `values` (`3 ≤ n ≤ 50`), bei dem `values[i]` das Gewicht des Vertex `i` eines konvexen `n`sided Polygons ist.
Eine Triangulation ist eine Reihe von `n‐2`-Dreiecks, deren Vertiken Vertikale das Polygon sind.
Die Punktzahl einer Triangulation = Summe des Produkts der Werte der drei Wirbel jedes Dreiecks.

Geben Sie das *minimum* mögliche Ergebnis zurück.

> **Beispiel**
> `Werte = [3,7,4,5]` → minimale Punktzahl = **144** (Triangulation: `(3,4,5)` + `(3,4,7)`).

---

Â 🧠 Intuition – „Matrix‐Chain Multiplication“ trifft Geometrie

Wenn Sie ein Sub-Polygon betrachten, das durch Vertices `i ... j` definiert ist, können Sie einen Scheitel `k` (`i < k < j`) als den dritten Scheitel eines Dreiecks auswählen, das den Rand `i‐j` verwendet.

`` `
I ----
| |
| |
`` `

Die Punktzahl dieses Dreiecks ist `Werte[i] * Werte[j] * Werte[k]`.
Das übrige Polygon wird in zwei unabhängige Unter-Polygone aufgeteilt: `i ... k` und `k ... j`.
So kann die minimale Punktzahl für `i ... j` rekursiv ausgedrückt werden:

`` `
dp[i][j] = min über k (dp[i][k] + dp[k][j] + Werte[i]*Werte[j]*Werte[k])
`` `

Wenn das Sub-Polygon nur zwei Vertiken hat (`j == i+1`), kann kein Dreieck gebildet werden → Punktzahl `0`.

Dies ist genau die Wiederholung, die in der Matrix‐Chain Multiplikation verwendet wird, nur der Begriff "Kosten" ist ein Produkt von drei Zahlen anstelle einer Matrix Multiplikation Kosten.

---

🏗️ Algorithm Design

Schritt | Aktion |
|-------------------
| 1 | Initialisieren Sie ein 2‐D-Array `dp[n][n]` mit `-1` (oder `∞` für Bottom‐up). |
| 2 | Rekursiv `dp[i][j] ` mit Memoization (top‐down) oder iterate über zunehmende Sub-Polygonlängen (unten-up). |
| 3 | Für jede `i < k < j` Bewertung von `score = dp[i][k] + dp[k][j] + Werten[i]*Werte[j]*Werte[k] `. |
| 4 | Speichern Sie das Minimum in `dp[i][j]`. |
| 5 | Ergebnis ist `dp[0][n-1]`. |

---

📦 Code in drei Sprachen

> **Anmerkung:** Alle Implementierungen folgen der gleichen Logik – top‐down memoization.
> Bottom‐up kann in Kommentaren hinzugefügt werden, wenn Sie eine iterative Version bevorzugen.

### 1️⃣ Java

``java
java.util importieren. Strahlen;

Public class Lösung {\cHFFFF}
Public int minScoreTriangulation(int[] Werte) {\cHFFFF}
int n = Werte.Länge;
int[][] dp = neu int[n][n][n];
für (int[] Zeile : dp) Arrays.fill(row, -1);
zurückgeben dfs(Werte, 0, n - 1, dp);
}

Private Int dfs(int[]-Werte, int i, int j, int[][] dp) {
wenn (i >= j - 1) 0 zurückgeben; // weniger als 3 Punkte
wenn (dp[i][j] != -1) Rückgabe dp[i][j;

int best = Integer.MAX_VALUE;
für (in k = i + 1; k < j; k++) {
int Kosten = Werte[i] * Werte[j] * Werte[k]
+ dfs(Werte, i, k, dp)
+ dfs(Werte, k, j, dp);
wenn (kosten < best) am besten = Kosten;
}
dp[i][j] = am besten;
Rückkehr am besten;
}
}
`` `

### 2️⃣ Python

```python
Klasse Lösung:
def minScoreTriangulation(Selbst, Werte: list[int]) -> int:
n = len(Werte)
memo = [[None] * n for _ in range(n)]

def dfs(i: int, j: int) -> int:
wenn i >= j - 1: # < 3 vertices
Rückkehr 0
wenn memo[i][j] nicht Keine:
zurück memo[i][j]

best = Float ("inf")
für k im Bereich (i + 1, j):
Kosten = (
Werte[i] * Werte[j] * Werte[k]
+ dfs(i, k)
+ dfs(k, j)
)
best = min(best, kosten)

memo[i][j] = am besten
zurück zur Übersicht

Rückgabe dfs(0, n - 1)
`` `

### 3️⃣ C++

```cpp
#include <vector>
#include <algorithm>
#include <climits>

Klasse Lösung {
öffentlich:
Int minScoreTriangulation(std::vector<int>&values) {\cHFFFF}
int n = Werte.size();
std::vector<std::vector<int> dp(n), std::vector<int>(n, -1));
zurückgeben dfs(Werte, 0, n - 1, dp);
}

privat:
Int dfs(const std::vector<int& v, int i, int j, std::vector<std::vector<int>>& dp) {
wenn (i >= j - 1) 0 zurückgeben; // weniger als 3 Punkte
wenn (dp[i][j] != -1) Rückgabe dp[i][j;

int best = INT_MAX;
für (in k = i + 1; k < j; ++k) {
Int Kosten = v[i] * v[j] * v[k]
+ dfs(v, i, k, dp)
+ dfs(v, k, j, dp);
best = std::min(best, Kosten);
}
dp[i][j] = am besten;
Rückkehr am besten;
}
};
`` `

---

📈 Komplexitätsanalyse

| Technik | Zeit | Raum |
|---------------------
| Top‐down-Memoization (alle 3 Codes) | **O(n3)* – `O(n2)` Sub‐Probleme, jede Scans `O(n)` Splits. | **O(n2)** – DP-Tabelle + Recursion Stack (`O(n)` Tiefe). |
| Bottom‐up (nicht gezeigt) | Gleiches | Gleiches |

Mit `n ≤ 50` passt der Algorithmus leicht in die Grenzen (≈125 000 Iterationen).

---

📜 “Das Gute, das Schlechte und das Böse”

| Kategorie | Diskussion |
|-------------------------
| **Good** | • Intuitive Recurrence – leicht zu verstehen. <br>• Erfordert nur `O(n2)` Speicher. <br>• Arbeitet für alle konvexe Polygone (keine versteckten Fälle). |
| **Bad** | • Die Zeit ist kubisch; für sehr große `n` würde es schwer werden (obwohl `n=50` ist gut). <br>• Das Produkt `Werte[i] * Werte[j] * Werte[k]` könnte 32-Bit-Int in Extremfällen überlaufen (wenn Werte größer waren). Im offiziellen Problem gebunden (`≤100`) ist es sicher. |
| **Ugly** | • Die DP-Rekursion ist *nicht* offensichtlich für Anfänger; sie können denken, “Matrix-Multiplikation” und verwirrt werden. <br>• Memoization braucht sorgfältiges Base-Case-Handling (`i >= j-1`). Ein Typo führt zu Stack-Überlauf oder falsche Antworten. <br>• In Sprachen mit kleinen Int-Bereichen (z.B. JavaScript) müssen Sie BigInt verwenden. |

**Take‐away:** Konzentrieren Sie sich auf ein klares Basisgehäuse, verwenden Sie bei Bedarf lange ganze Zahlen und Testrandfälle (`n=3`, alle gleichen Werte, aufsteigende/absteigende Arrays).

---

SEO‐Optimierte Blog Titel & Meta Beschreibung

**Titel:**
> “Minimum Score Triangulation von Polygon – LeetCode 1039 | Java, Python, C++ Solutions“

**Meta Beschreibung:**
> „Lesen Sie, wie man LeetCode 1039 (Minimum Score Triangulation of Polygon) mit top‐down Memoization löst. Voller Java-, Python- und C++-Code, Komplexitätsanalyse und ein tiefer Tauchgang in die guten, schlechten und hässlichen DP-Lösungen. „

---

Letzte Gedanken

- Warum DP? Da die optimale Triangulation eines Sub-Polygons nur von seinen Endpunkten abhängt, ist eine perfekte Passform für Intervall DP.
- Warum memoization? Recursion hält den Code sauber, und die Problemgröße (`n ≤ 50`) garantiert keine Stapelprobleme.
- **Wann nach unten wechseln?** Wenn Sie eine Rekursion für sehr tiefe Rekursionsgrenzen vermeiden oder die DP-Tabelle explizit vorordnen möchten.

Mit den Code-Snippets und Erläuterung oben, Sie können zuversichtlich anpacken **LeetCode 1039** in Interviews, Blog-Posts oder Codieren Wettbewerbe. Glückliche Kodierung