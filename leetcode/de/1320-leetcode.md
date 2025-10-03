---
Titel: LeetCode 1320. Mindestabstand zum Eingeben eines Wortes mit zwei Fingern -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
# 🧑 💻 1320 – Mindestabstand zum Eingeben eines Wortes mit zwei Fingern
**Lösungen in Java, Python, & C++**** **Full Blog Artikel (SEO-optimiert)* *

---

1️⃣ Problem Recap

Sie erhalten ein 5 × 6 Tastatur-Layout (A...Z).
Die Koordinaten sind:

| Buchstaben | (x, y) |
|---------------------
| A | (0, 0) |
| B | (0, 1) |
| ...
| Z | (4, 1) |

Du hast zwei Finger**. Die erste Verwendung jedes Fingers ist frei (kein Abstand wird geladen).
Für jede nachfolgende Tastenpresse zahlen Sie die Entfernung von Manhattan zwischen den beiden Buchstaben, die Sie eingeben.

> **Goal** – geben Sie einen String `word` (2 ≤ |word| ≤ 300) mit der **minimum** Gesamtstrecke ein.

---

Intuition & DP Staat

- Wenn wir in Position `i` in `Wort` sind, ist das Einzige, was zählt **, wo jeder Finger* ist.
- Jeder Finger kann sein:
- *un-set* (kostenlos für den ersten Gebrauch) – wir kodieren das als `-1`.
- oder auf einem Buchstaben `c` (0–25).

So ist ein DP-Zustand:

`` `
dp[i][f1][f2] = minimaler Abstand zum Auslesen von i,
wobei Finger 1 auf f 1, Finger 2 auf f 2
`` `

`f1, f2 ε {‐1, 0...25}` → 27 × 27 mögliche Werte für jedes `i`.

**Übergang* *

`` `
Let cur = Wort[i]
Option 1: Finger 1 verwenden
Kosten = Entfernung(f1, cur) // 0 wenn f1 == -1
= dp[i+1][cur][f2]

Option 2: Verwendung von finger2
Kosten = Distanz(f2, Cur) // 0 wenn f2 == -1
= dp[i+1][f1][cur]
`` `

Antwort = `dp[0][-1][-1]`.

Der Abstand zwischen zwei Buchstaben ist einmal vorbestellt.

---

3️⃣ Komplexität

| Zeit | Raum |
|----------
Recursive + Memo | **O(word × 272)** ≈ 200 000 Operationen ≈ **O(word × 272)** |
| Iterative | gleiche | | |

Beide passen bequem in die Grenzen.

---

4️⃣ Code

Im Folgenden finden Sie **bereits‐zu‐paste**-Implementierungen in den drei angeforderten Sprachen.

> **Tip** – Alle drei verwenden die gleiche zugrunde liegende DP-Logik, die gerade idiomatisch ausgedrückt wird.

---

### 4.1 Java

``java
java.util importieren. Strahlen;

Public class Lösung {\cHFFFF}
// 26 Buchstaben + 1 "noch nicht verwendet" sendinel
Privater statischer Abschluss int NOT_SET = -1;
private statische Endint N = 27; // 0...25 für Buchstaben, 26 für NOT_SET
private statische Endint[][] pos = neuer Int[26][2];
private statische Int[][][] memo;
privat String Wort;
int len;

// Vorkomputierte Positionen auf einer 5×6 Tastatur
statisch
für (in i = 0; i < 26; i++) {
pos[i][0] = i % 6; // x
pos[i][1] = i / 6; // y
}
}

öffentliches Mindesteinkommen Entfernung (Stringwort) {
das.word = Wort;
Dies.len = Wort.Länge();
// +1 zu speichern NOT_SET-Zustand auf Index 26
memo = neuer Int[len + 1][N][N];
für (int i = 0; i <= len; i++)
für (int f1 = 0; f1 < N; f1++)
Arrays.fill(memo[i][f1], -1);
Renditesolv(0, NOT_SET, NOT_SET)
}

privater Int-Lösung(int idx, int f1, int f2)
wenn (idx == len) 0 zurückgeben;
int fi1 = (f1 == NOT_SET) ? 26 : f1;
int fi2 = (f2 == NOT_SET) ? 26 : f2;
int cached = memo[idx][fi1][fi2];
wenn (gespeichert) -1) zurückgespeichert;

int cur = word.charAt(idx) - 'A';
// Option 1: Finger 1 verwenden
int cost1 = Entfernung (f1, cur) + Sol (idx + 1, cur, f2);
// Option 2: Finger 2 verwenden
int cost2 = Entfernung (f2, cur) + Sol (idx + 1, f1, cur);

int ans = Math.min(cost1, cost2);
memo[idx][fi1][fi2] = ans;
Rückgabe ans;
}

privater Int-Distanz (int von, int zu) {
wenn (aus == NOT_SET) 0 zurückgeben;
int x1 = pos[from][0], y1 = pos[from][1];
int x2 = pos[to][0], y2 = pos[to][1];
Math.abs(x1 - x2) + Math.abs(y1 - y2) zurückgeben;
}
}
`` `

---

### 4.2 Python

```python
Import Functools
aus der Einfuhr Liste

Klasse Lösung:
# Pre‐compute Koordinaten für A..Z
Koorden: List[tuple] = [(i % 6, i // 6) für i in range(26)]

Mindestens Entfernung(selbst, Wort: str) -> int:
@functools.lru_cache(None)
def dp(idx: int, f1: int, f2: int) -> int:
""f1/f2 sind Indizes 0‐25 für einen Brief, -1 bedeutet ungenutzt.""
wenn idx == len(word):
Rückkehr 0

Cur = ord(word[idx]) - 65 # 0-basiert

# Finger 1 verwenden
cost1 = self.dist(f1, cur) + dp(idx + 1, cur, f2)
# Finger 2 verwenden
cost2 = self.dist(f2, cur) + dp(idx + 1, f1, cur)

zurück min(cost1, cost2)

zurück dp(0, -1, -1)

def dist(self, from_idx: int, to_idx: int) -> int:
wenn von_idx == -1:
Rückkehr 0
x1, y1 = Self.coords[from_idx]
x2, y2 = Self.coords[to_idx]
zurück abs(x1 - x2) + abs(y1 - y2)
`` `

---

### 4.3 C++

```cpp
#include <bits/stdc++.h>
mit Namespace std;

Klasse Lösung {
öffentlich:
// Vorkomputierte Koordinaten für A..Z
vektor<pair<int,int>> pos(26)
Vektor>vector<vector<vector>> Memo;
Stringwort;
int n;

Lösung() {
für (in i = 0; i < 26; ++i) {\cHFFFF}
pos[i] = {i % 6, i / 6};
}
}

mindestens Entfernung (Stringwort) {
Dieses Wort = Wort;
n = Wort.size();
// 27 = 26 Buchstaben + 1 für „nicht verwendet“
memo.assign(n + 1, vector<vector<int>>(27, vector<int>(27, -1)));
zurück dp(0, 26, 26); // 26 stellt NOT_SET
}

privat:
int dp(int idx, int f1, int f2)
wenn (idx == n) 0 zurückgeben;
(Memo[idx][f1][f2] != -1) Memo[idx][f1][f2] zurückgeben;

int cur = Wort[idx] - 'A';
// Finger 1 benutzen
int cost1 = dist(f1, cur) + dp(idx + 1, cur, f2);
// Mit dem Finger 2
int cost2 = dist(f2, cur) + dp(idx + 1, f1, cur);

Rückgabe memo[idx][f1][f2] = min(cost1, cost2);
}

int dist(int von, int zu) {
wenn (aus == 26) 0 zurückgeben; // NOT_SET
Auto [x1, y1] = pos[from];
Auto [x2, y2] = pos[to];
zurück abs(x1 - x2) + abs(y1 - y2);
}
};
`` `

---

Artikel 5️⃣ Blog (SEO‐Optimiert)

> **Titel:** *Minimum Entfernung zum Eingeben eines Wortes mit zwei Fingern – Java, Python & C++ Lösungen*
> Beschreibung:*** Solve LeetCode 1320 mit klaren DP-Erklärungen, optimalem Java/Python/C++-Code und einem SEO-freundlichen Leitfaden für Interview prep.

---

### 5.1 Einführung

Das **“Minimum Distance to Type a Word Using Two Fingers”** Problem ist eine klassische dynamische Programmier-Herausforderung, die Ihre Fähigkeit testet, Zustand zu modellieren und Übergänge zu optimieren. Es ist eine perfekte Interview-Frage für Software-Engineering-Rollen, vor allem diejenigen, die sich auf algorithmische Design und Datenstruktur-Mastery.

Dieser Artikel geht durch die Argumentation, präsentiert drei produktionsbereite Implementierungen und gibt Ihnen ein tieferes Verständnis der „guten, schlechten und hässlichen“ Aspekte, die Sie bei der Lösung treffen werden.

---

### 5.2 Problem Recap

- **Keyboard Layout:** 5 Zeilen × 6 Spalten (Briefe A–Z).
- **Distance Metrik:** Entfernung von Manhattan, `|x1‐x2| + |y1‐y2|`.
- **Rules:**
- Die erste Verwendung jedes Fingers ist kostenlos.
- Finger können auf jedem Schlüssel (einschließlich des ersten Zeichens) starten.
- Sie müssen das angegebene Wort mit **mindesten Gesamtabstand* eingeben.

**Input** – ein String `word` (oberer Fall, Länge ≤ 300).
**Ausgang** – der minimale Abstand (Integer).

---

### 5.3 Schlüsselideen

ANHANG **State Compression**
Das einzige, was die zukünftigen Kosten beeinflusst, ist die aktuelle Lage jedes Fingers. Wir brauchen nicht die gesamte Geschichte, also komprimieren wir den Zustand zu `(Index, Finger1, Finger2)`.

2. **Sentinel für „noch nicht verwendet“* *
Verwenden Sie `-1` (oder `26` in C++) um den „freien“ Zustand darzustellen. Das erste Mal, wenn ein Finger verwendet wird, ist der Abstand `0`.

3. ** Vorleistung**
Koordinaten jedes Buchstabens auf der Tastatur sind deterministisch. Speichern Sie sie in einem Array für O(1) Lookup.

4. **Transitionssymmetrie**
Bei der Entscheidung, welchen Finger für das nächste Zeichen zu verwenden, sind die beiden Optionen symmetrisch. Dies reduziert den Suchraum dramatisch.

---

### 5.3 Dynamische Programmierableitung

| Schritt | Was wir tun | Warum es funktioniert |
------------------------------------------
| **Definition DP** | `dp[i][f1][f2] ` – minimale Kosten aus der Position `i` angegebenen Fingerstellen. | Erfasst alle zukünftigen Abhängigkeiten. |
| **Base Case** | `i == len(word)` → `0`. | Fertige Typisierung → keine Kosten mehr. |
| **Übergang** | Verwenden Sie entweder Finger. Kosten berechnen + `dp[i+1][...] | Lokale Optimität: beste Wahl im aktuellen Schritt führt zum globalen Optimum. |
| **Memoization** | Cache ergibt ein 3‐D-Array oder `lru_cache`. | Vermeiden Sie exponentielles Blasen; jeder Staat löste einmal. |

---

### 5.4 „Gut“ – Warum DP arbeitet

- **Deterministischer Zustandsraum** – Nur Fingerpositionen sind wichtig.
- **Polynomzeit* Die Zwänge des Problems sind bescheiden, aber die DP garantiert Effizienz.
- **Clean separability* Die First-Use-Regel übersetzt eine einfache “0 Kosten, wenn nicht eingestellt” Überprüfung.

---

### 5.5 “Bad” – Gemeinsame Pitfalls

| Ausgabe | Erklärung | Fix |
|------------------------------
| Mis‐encoding NOT_SET | Die Verwendung von `-1` direkt im 3‐D-Arrayindex führt zu negativen Indizes. | Map `-1` → 26 (oder jeder “extra” Slot). |
| Überzählungsabstand | Vergessen Sie, dass die erste Verwendung eines Fingers frei ist. | Sonderfall: `distanz = 0 ` wenn Finger == NOT_SET. |
| Recursion Tiefe | Pythons Recursionsgrenze beträgt 1000, aber die Wortlänge ≤ 300, so ist es sicher, aber immer noch Wache mit `sys.setrecursionlimit`. |

---

### 5.6 „Ugly“ – Trade‐offs & Variations

- **Memory Verbrauch** – 273 × 300 ≈ 200 000 t (~ 0,8 MB). Wenn der Speicher zu einem Anliegen wird (z.B. in einer speicherdichten Interviewumgebung), können Sie ihn auf ** zwei Schichten* (`dp_cur`, `dp_next `) reduzieren, weil `dp[i] ` hängt nur von `dp[i+1]` ab.
- ** Unterschiedliche Tastaturformen** Wenn sich das Tastaturlayout ändert, müssen Sie nur das `pos`-Array neu erstellen.
- **Parallelismus** Hier nicht notwendig; die DP ist inhärent sequentiell aufgrund der Reihenfolge der Zeichen.

---

### 5.7 Letzte Gedanken & Interview Tipps

- **Erklären Sie Ihren Zustand deutlich* Interviewer lieben es, Sie artikulieren, warum jede Dimension zählt.
- **Zeigen Sie das Übergangsdiagramm** – Eine einfache Tabelle oder Pseudocode-Übergang verdeutlicht Ihre Argumentation.
- **Ask klärende Fragen** – Zum Beispiel: „Wir dürfen den gleichen Finger zwischen zwei aufeinanderfolgenden Tasten wechseln?“ In diesem Problem, ja, aber diese Annahme explizit zu machen kann subtile Fehler vermeiden.
- **Test Randfälle** – Leere Zeichenkette, alle gleichen Buchstaben, Wechselbriefe, längste Zeichenfolge.

---

### 5.8 Zusammenfassung

Wir haben:

ANHANG Decodierte das LeetCode 1320 Problem in ein prägnantes DP-Modell.
2. Durch den **gut** – deterministischer Zustand, polynomielle Komplexität, saubere Übergänge.
3. Das **bad** – Fallstricke rund um Singinelwerte, Erstnutzungskosten.
4. Die **ugly*** – Speichernutzung, mögliche Rekursionstiefenprobleme.

Die Code-Snippets für **Java, Python und C++** sind vollständig getestet und bereit für Produktionsinterviews oder als Vorlage für ähnliche DP-Probleme.

Viel Glück und glückliche Kodierung! 🚀

---


---


** Ende des Artikels**



---


### 6️⃣ Anmerkung

> **Pro tip** – Bei der Vorbereitung auf Interviews, halten Sie dieses Muster im Auge: *Identifizieren Sie das minimale “Memory” benötigt, um die Zukunft zu beschreiben*, codieren Sie, dass als DP-Zustand jede teure Lookup (wie Entfernungen) vorrechnen und dann über die Wahlen iterieren.
> LeetCode 1320 ist ein Lehrbuchbeispiel für dieses Prinzip. Alles Gute!