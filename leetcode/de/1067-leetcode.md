---
Titel: LeetCode 1067. Digit Count in Range -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
oder 1. LeetCode 1067 – **Digit Count in Range* *
**Problem*** | `öffentliche Int-Zeichen Anzahl d, int niedrig, int hoch `
** Schwierigkeit***

> **Goal** – Für eine einzelne Ziffer `d (0‐9) und einen inklusiven Bereich `[low, high]`, geben Sie die Gesamtzahl der Zeiten `d` in den dezimalen Darstellungen jeder Ganzzahl in diesem Bereich zurück.
> **Beschränkungen* – `1 ≤ niedrig ≤ hoch ≤ 2·108` (≈ 200 Mio.).

Da der Eingangsbereich riesig sein kann, wäre eine naive Schleife (`for (int i=low;i<=high;i++) ...`) viel zu langsam. Die Standardlösung verwendet **digit‐DP** – eine dynamisch-programmierende Technik, die die Dezimalstellen einer Anzahl von am bedeutendsten bis am wenigsten bedeutungsvollen verarbeitet und dabei die „dichten“ und „leading‐zero“ Zustände aufrecht erhält.

Im Folgenden finden Sie Arbeits-, Annotierte Implementierungen in **Java, Python und C++**, die in `O(log N)` Zeit und `O(log N)` Speicher laufen.

---

oder 2. Java Implementierung (Digit‐DP)

``java
/**
* LeetCode 1067 – Digit Count in Range
*
* Java 17, O(log N) Zeit, O(log N) Speicher
*
Klasse Lösung {
// Memoization table: pos x count
Private Int[][] memo;
privates Int-Ziel; // ziffern wir
Private char[] Ziffern; // String-Darstellung der aktuellen Nummer

int digitals Anzahl d, int niedrig, int hoch
das. Ziel = d;
CountUpTo(high) - countUpTo(low - 1);
}

/** Anzahl der Zielvorkommen in [0, n] */
Private Int CountUpTo(int n) {\cHFFFF}
wenn (n < 0) 0 zurückgeben; // Schutz für low-1
Ziffern = Integer.toString(n).toCharArray();
int len = Ziffern. Länge
memo = new int[len][len]; // maximale Vorkommen <= len
für (int[] Zeile : memo) Arrays.fill(row, -1);
zurückgeben dp(0, 0, true, false);
}

/**
* @param pos aktueller Index in Ziffern[]
* @param cnt Anzahl der Zielziffern bisher gesehen
* @param dicht, ob frühere Ziffern das Präfix von n
* @param begann, ob wir noch eine nicht führende Nullstelle platziert haben
* @Return totale Ziel-stellige Ereignisse aus diesem Zustand weiter
*
privat int dp(int pos, int cnt, boolean eng, boolean gestartet) {\cHFFFF}
wenn (pos == digits.length) cnt zurückgeben; // Ende der Nummer
wenn (!tight && start && memo[pos][cnt] != -1) // Cache hit
zurück memo[pos][cnt];

int limit = eng ? Ziffern[pos] - '0' : 9;
int total = 0;

// Option 1: Diese Position überspringen (noch führende Nullen)
wenn (!started) insgesamt += dp(pos + 1, cnt, false, false)

In den Warenkorb Digit = gestartet ? 0 : 1; // keine führende Null erlaubt nach Start
für (int d = startDigit; d <= limit; d++) {\cHFFFF}
In den Warenkorb Cnt = cnt + (d == Ziel ? 1 : 0);
boolean newTight = eng && (d == Grenze);
Gesamt += dp(pos + 1, newCnt, newTight, true);
}

wenn (!tight & gestartet) memo[pos][cnt] = gesamt;
Gesamtsumme;
}
}
`` `

### Wie es funktioniert

| Schritt | Was passiert |
|------------------------
| `digitsCount` | Calls Helper for `high` und `low-1`, dann Subtraktionen. |
| `countUpTo` | Konvertiert `n` in Char-Array, bereitet Memo vor, ruft `dp`. |
| `dp` | Erforscht alle möglichen Ziffern an Position `pos`. |
| Zustand | `(pos, cnt, eng, gestartet)` |
| Memoization | Speichert Ergebnisse für *nicht-dicht* Zustände, um Recomputation zu vermeiden. |

Der Algorithmus besucht maximal `len * len` Zustände (`len ≤ 10` für 2·108), so ist es praktisch konstante Zeit.

---

oder 3. Python Implementierung (One-Line DP)

```python
# LeetCode 1067 – Digit Count in Range
# Python 3.11, O(log N) Zeit, O(1) Speicher (explicit using recursion limits)
Klasse Lösung:
def Ziffern Count(self, d: int, low: int, high: int) -> int:
zurück self.f(high, d) - self.f(low - 1, d)

def f(self, n: int, Ziel: int) -> int:
wenn n < 0: Rückkehr 0
s = s
m = len(s)
memo = [[-1] * (m + 1) für _ in range(m)]

def dp(i: int, cnt: int, fest: bool, gestartet: bool) -> int:
wenn i == m:
zurück
wenn nicht fest und gestartet und memo[i][cnt] != -1:
zurück memo[i][cnt]
bis = Int(s[i]) wenn dicht noch 9
= 0
wenn nicht gestartet:
res += dp(i + 1, cnt, False, False) # Überspringen
zum Ausgraben im Bereich(0 wenn noch 1, bis + 1):
res += dp(i + 1, cnt + (dig == ziel), eng und grab == up, True)
wenn nicht fest und gestartet:
memo[i][cnt] = res
zurück

zurück dp(0, 0, Wahr, Falsch)
`` `

> **Warum Python funktioniert* – Pythons Rekursionstiefe kann 10 Levels (max. Zahlen) verarbeiten.
> **Space*** – `memo` ist höchstens `10 × 10`.
> **Zeit** – Noch `O(log N)`.

---

oder 4. C++ Implementierung (Bottom‐Up Digit DP)

```cpp
// LeetCode 1067 – Digit Count in Range
// C++17, O(log N) Zeit, O(log N) Speicher
#include <bits/stdc++.h>
mit Namespace std;

Klasse Lösung {
öffentlich:
int Ziffern Anzahl d, int niedrig, int hoch
Ziel = d;
CountUpTo(high) - countUpTo(low - 1);
}

privat:
Int-Ziel;
Vektor<int>-Zeilen;
Vektor<vector<int>>> memo; // memo[pos][cnt]

Int CountUpTo(int n) {\cHFFFF}
wenn (n < 0) 0 zurückgegeben wird;
digits.clear();
während (n) { digits.push_back(n % 10); n /= 10; }
reverse(digits.begin(), digits.end()); // bedeutendste erste
int len = digits.size();
memo.assign(len, vector<int>(len + 1, -1));
zurückgeben dfs(0, 0, true, false);
}

int dfs(int pos, int cnt, bool eng, bool gestartet) {\cHFFFF}
wenn (pos == digits.size()) cnt zurückgegeben wird;
wenn (!tight && start && memo[pos][cnt] != -1) Memo[pos][cnt] zurückgeben;

int limit = eng ? Ziffern[pos] : 9;
int res = 0;

wenn (!started) res += dfs(pos + 1, cnt, false, false) res; // Null überspringen

In den Warenkorb Digit = gestartet? 0 : 1;
für (int dig = start Digit; dig <= limit; ++dig) {
res += dfs(pos + 1, cnt + (dig == Target), eng && dig == Limit, true);
}

wenn (!tight & gestartet) memo[pos][cnt] = res;
zurück;
}
};
`` `

> **Key Unterschiede** Verwendet einen expliziten Vektor für Ziffern, Bottom-up-Recursion (keine Lambdas).
> **Komplexität** – Identical to Java/Python: `O(log N)` Zeit, `O(log N)` Speicher.

---

oder 5. Blog Artikel – „Das Gute, Das Schlechte, Die Ugly von Digit‐DP auf LeetCode 1067“

> **Keywords*: LeetCode 1067, Digit Count in Range, Digit DP, dynamische Programmier-Interview-Fragen, Job-Interview, Software-Ingenieur, Java-Lösung, Python-Lösung, C++-Lösung, Codierung Interview, Algorithmus-Design

### 5.1 Das Problem in einer Nutshell

LeetCode 1067 bittet Sie zu zählen, wie oft eine einzelne Ziffer innerhalb eines riesigen Ganzzahlintervalls erscheint. Der Eingang kann so groß wie 200 Millionen sein, aber Sie müssen unter einer Millisekunde beenden. Auf den ersten Blick scheint eine brute‐force-Schleife wie die natürliche Antwort – einfach iterieren und jede ganze Zahl in einen String umwandeln, aber das würde *hundreds of millions of string Conversions* erfordern, unmöglich in einem Interview oder einer Codierungs-Herausforderung.

Das ist das klassische Problem der Zählung von Ziffern in einer Reihe. Die elegante Lösung ist *digit‐DP* – ein dynamisch-programmierender Ansatz, der das Problem als Traversal der Dezimalstellen der Randnummern behandelt.

### 5.2 Das Gute – Warum Digit‐ DP ist der Goldstandard

| Warum es scheint | Erklärung |
|---------------------------
| **Optimale Zeit* | Runs in `O(log N)` pro Abfrage (≤ 10 Ziffern für `2·108`). |
| **Simplicity with recursion** | Jeder Recursionsschritt handhabt eine einzelne Zahl; der Zustand ist winzig: Position, bisher gezählt, enge Flagge, führende‐Null-Flagge. |
| ** Wiederverwendbar über Probleme** | Sobald Sie digital‐ DP, Sie können eine Vielzahl von Problemen lösen: “zählen Zahlen mit einer bestimmten Summe von Ziffern”, “Zahlen divisible by K”, “count palindromes in range”, etc. |
| **Memory-friendly** | Memoization table size is `digits × digits` (≤ 100 ganze). |

> **Interview Tip** – Vorlage des Zustandsdiagramms zuerst. Zeigen Sie, dass es nur 4 logische Zustände gibt: `tight` (präfix gleich der Grenze) und `started` (ob wir eine nicht-Null-stellige Stelle platziert haben). Das macht die Rekursion offensichtlich.

### 5.3 The Bad – Common Pitfalls and How to Avoid Them

ANHANG **Leading Zeros* – Vergessen, führende Nullen zu behandeln, besonders verursacht das Überzählen von Ziffern wie `0013`.
*Solution*: Fügen Sie eine "started"-Flag hinzu; nur `target` zählen, wenn `started` wahr ist, ansonsten springen.

2. ** Off‐by‐One on Ranges** – Viele Lösungen subtrahieren `count(low-1)`, vergessen aber, dass `low-1` vielleicht `0` sein könnte.
*Solution*: Wärter hinzufügen `if (n < 0) zurück 0; ` im Helfer.

3. **Memoization Konditionen** – Das Speichern von Ergebnissen für *dichte* Zustände ist falsch, weil sich die obere Grenze pro Anruf ändert.
*Solution*: Memo nur für `!tight && start`.

4. **Recursion Depth* – In Sprachen mit flachen Rekursionsgrenzen (z.B. Python 2) kann `sys.setrecursionlimit` benötigt werden.
*Solution*: In Python ist die Rekursionstiefe nur 10 für dieses Problem, aber gesetzte Grenze sowieso, wenn Sie verallgemeinern.

5. **Wrong Digit Order** – Die Umrechnung einer Nummer in einen String im Vergleich zum Aufbau einer Reihe von Ziffern von am wenigsten bis maximal kann die Bedeutung von `pos` umkippen.
*Solution*: Standardisieren auf **most‐significant first**; es vereinfacht die `tight` Fahnenlogik.

### 5.4 The Ugly – Edge Cases, die selbst Experten auf Reisen

| Edge Fall | Warum es böse ist | Fix |
---------------------------------------
| **d = 0** | Führende Nullen nie gezählt, so erscheint 0 nur in Zahlen wie 10, 20... aber *not* als führende Zahl von 100. | Halten Sie die "started"-Flag; `target` nur, wenn `started`. |
| **Range enthält 1** | `low = 1` gibt `high-low+1 = 1` ganze Zahl, aber der Helfer funktioniert immer noch, weil `countUpTo(0)` 0 ist. | Keine Änderung – der `countUpTo(low-1)` Guard handhabt es. |
| **high = 2·108** | 9-stellige Zahlen, aber einige Sprachen behandeln 200 000 000 000 als 9 Ziffern; stellen Sie sicher, dass die Länge der Ziffern korrekt ist. | Konvertieren Sie in String oder verwenden Sie Divisionsschleife; sie geben beide die richtige Länge. |
| **target = 0 und Zahl = 0** | 0 enthält eine Null. Einige Lösungen überspringen irrtümlich die Zählung aufgrund der `started`-Flag. | Sonderfall: wenn `n == 0 && Ziel == 0`, zurück 1. |

### 5.5 SEO‐ Optimierte Zusammenfassung für Jobsuchende

> **Wenn Sie sich auf ein Software-Engineering-Interview vorbereiten, digital‐ beherrschen DP löst nicht nur LeetCode 1067 in Millisekunden, sondern zeigt auch tief algorithmisches Denken. **
> **Ein sauberes Java, Python oder C++ Implementierung von digit‐ DP*** wird Interviewer beeindrucken, die erwarten, dass Sie große Eingabeprobleme effizient bewältigen.
> **Beyond LeetCode, Digi‐DP-Konzepte erscheinen in real‐world-Szenarien** – Vorherrschende Algorithmen, kombinatorische Zählung in Analytik und sogar beim Aufbau effizienter Suchindexe.

**Mitnahme für den Lebenslauf:**

- * Dynamische Programmierung:* Bewährte Expertise in DP-Mustern.
- *Time‐Komplexitätsoptimierung:* Gelieferte Lösungen in `O(log N)`.
- *Cross‐Language Effizienz:* Java, Python, C++ Lösungen mit der gleichen Logik.
- *Problem Lösen:* Harte Interview-Fragen wie “Digit Count in Range” schnell anfassen.

Verwenden Sie die Phrase **“Digit‐DP-Algorithmus-Design”** im Kompetenzbereich; Rekrutierer verwenden sie oft als Keyword-Filter.

---

oder 6. Schluss

Die oben genannten Lösungen sind bereit, in Ihre IDE- oder Codierungsplattform zu kopieren. Wenn Sie sie in einem Interview präsentieren, gehen Sie durch die Zustandsmaschine, erklären Sie die Handhabung der führenden Nullen, und betonen die `tight` Flagge. Diese Erzählung, verbunden mit dem eleganten rekursiven Code, lassen Interviewer überzeugt, dass Sie ein starker Kandidat für jede Software-Engineering-Rolle. 🚀

---

*Happy Codierung! *