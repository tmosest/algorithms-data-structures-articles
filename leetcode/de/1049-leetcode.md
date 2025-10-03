---
Titel: LeetCode 1049. Letztes Steingewicht II -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
# 1049. Letztes Steingewicht II – Code + SEO‐Optimierte Blog Post

oder 1. Problem-Recap (LeetCode 1049)

Sie erhalten ein Array `stones[]` von positiven Zahlen.
In einer Bewegung wählen Sie zwei Steine von Gewichten `x ≤ y`, zerschlagen sie:

| x = y | Ergebnis |
|--------------------
| true | Beide Steine verschwinden |
| false Der Stein des Gewichts `x` wird zerstört, der Stein des Gewichts `y` wird `y - x` |

Der Prozess geht weiter bis maximal ein Stein bleibt.
Gib das **smallest mögliche** Gewicht dieses Steins zurück (oder `0`, wenn keine).

Einschränkungen
- `1 ≤ Steine.Länge ≤ 30`
- `1 ≤ Steine[i] ≤ 100`

Da das Array winzig ist, ist eine dynamisch-programmierende Lösung basierend auf der **subset‐sum / 0‐1 knapsack** Idee perfekt.

---

oder 2. Core Idea – “Split die Steine in zwei Pfähle”

Das Ergebnis des Zerschlagens aller Steine kann als Aufteilung des Satzes in zwei Gruppen gedacht werden:

- Die Gruppe **A** (Gesamtgewicht `s1 `) wird gegen **B** (Gesamtgewicht `s2 `s2 `) zerschlagen.
- Nach allen Smashings ist das verbleibende Gewicht `|s1 – s2|`.

So wollen wir **minimise** `|s1 – s2|`.
Wenn wir `total = sum(stones)` lassen, dann `s2 = total – s1`.
Das Ziel wird:

`` `
min | insgesamt – 2 * s1 |
`` `

wobei `s1` ein Gewicht sein muss, das durch eine Untermenge von `stones` erreichbar ist.
Das ist genau das klassische **subset‐sum* (0‐1 knapsack) Problem.

### Warum das funktioniert

- Ja. Jeder Smash ist gleich, einen Stein von einer Gruppe zu nehmen und ihn von der anderen zu subtrahieren.
- Nach allen Operationen ist das verbleibende Steingewicht der absolute Unterschied der beiden Gruppensummen.
- Ja. Der minimal mögliche Unterschied ergibt sich, indem die Teilmenge am nächsten `total / 2` gefunden wird.

---

oder 3. Implementierungen

Unten sind saubere, idiomatische Lösungen in **Java, Python und C++**.
Alle verwenden **unt‐up DP** mit einem 2‐D-Booleantisch `dp[i][j]` – „Können wir die Summe `j` mit den ersten `i` Steinen machen?“
Zeit: `O(n * insgesamt) `
Raum: `O(n * insgesamt)` (kann mit einem 1‐D-Array auf `O(total)` reduziert werden, aber die 2‐D-Version hält die Logik kristallklar).

### 3.1 Java

``java
/**
* LeetCode 1049 – Letztes Steingewicht II
* DP-Lösung – O(n * Gesamtzeit, O(n * Gesamtfläche)
*
Public class Lösung {\cHFFFF}
int lastStoneWeightII(int[] stones) {\cHFFFF}
int n = Steine.Länge;
int total = 0;
für (int w : Steine) insgesamt += w;

// dp[i][j] = wahr, wenn wir die Summe j mit ersten i Steinen erreichen können
Boolean[][][] dp = neuer Boolean[n + 1][insgesamt + 1];
für (int i = 0; i <= n; i++) dp[i][0] = true; // Summe 0 ist immer möglich

für (in i = 1; i <= n; i++) {
int w = Steine[i - 1];
für (int j = 1; j <= total; j++) {\cHFFFF}
wenn (w <= j)
dp[i][j] = dp[i - 1][j]
} auch
dp[i][j] = dp[i - 1][j]
}
}
}

int best = Integer.MAX_VALUE;
// Suche nach der am nächsten liegenden Subsetsumme/2
für (int s = 0; s <= total / 2; s++) {
wenn (dp[n][s]) {\cHFFFF}
int diff = Math.abs(gesamt - 2 * s);
best = Math.min(best, diff);
}
}
Rückkehr am besten;
}
}
`` `

---

### 3.2 Python

```python
Klasse Lösung:
def lastStoneWeightII(self, stones: List[int]) -> int:
Gesamt = Summe(Stein)
n = len(Stein)

# dp[i][j] – können wir die Summe j mit ersten i Steinen erreichen?
dp = [[False] * (gesamt + 1) für _ im Bereich(n + 1)]
für i im Bereich(n + 1):
dp[i][0] = Wahr

für i im Bereich(1, n + 1):
w = Steine[i - 1!
für j im Bereich (1, insgesamt + 1):
wenn w <= j:
dp[i][j] = dp[i - 1][j] oder dp[i - 1][j - w]
andere:
dp[i][j] = dp[i - 1][j]

best = Float ("inf")
für s im Bereich(insgesamt // 2 + 1):
wenn dp[n][s]:
best = min(best, abs(gesamt - 2 * s))

zurück zur Übersicht
`` `

*(Python-Entwickler bevorzugen oft einen 1‐D DP für Speicherersparnisse: `dp[j] = dp[j] oder dp[j - w]`.) *

---

### 3.3 C++

```cpp
/**
* LeetCode 1049 – Letztes Steingewicht II
* DP-Lösung – O(n * Gesamtzeit, O(n * Gesamtfläche)
*
Klasse Lösung {
öffentlich:
int lastStoneWeightII(vector<int>& stones) {\cHFFFF}
int total = 0;
für (int w : Steine) insgesamt += w;
int n = stones.size();

vektor<vector<bool>> dp(n + 1, vektor<bool>(total + 1, false));
für (int i = 0; i <= n; ++i) dp[i][0] = true;

für (in i = 1; i <= n; ++i) {\cHFFFF}
int w = Steine[i - 1];
für (int j = 1; j <= total; ++j) {
wenn (w <= j)
dp[i][j] = dp[i - 1][j]
} auch
dp[i][j] = dp[i - 1][j]
}
}
}

int best = INT_MAX;
für (int s = 0; s <= total / 2; ++s) {
wenn (dp[n][s]) {\cHFFFF}
am besten = min(best, abs(gesamt - 2 * s));
}
}
Rückkehr am besten;
}
};
`` `

*(Erweiterte C++-Benutzer können den 2‐D DP durch einen einzigen Bitsatz ersetzen: `std::bitset<10001> dp; dp[0] = 1; für (Auto w : stones) dp |= dp << w; `, die in ~O(n * total / 64) Zeit läuft.) *

---

oder 4. Komplexitätsanalyse

| Implementierung | Zeit | Raum |
|---------------------------
| Java 2‐D DP | `O(n * insgesamt)` | | `O(n * insgesamt)` |
| Python 2‐D DP | `O(n * insgesamt)` | | `O(n * insgesamt)` |
| C++ 2‐D DP | `O(n * insgesamt)` | | `O(n * insgesamt)` |
| Bitset / 1‐D DP | `O(n * total / wordSize)`` | | `O(total)` |

Mit `n ≤ 30` und `total ≤ 3000` (30 * 100) sind diese Laufzeiten leicht schnell genug für LeetCodes Grenzen.

---

oder 5. Blog Post – *Das Gute, das Schlechte und die Ugly von “Letzte Stein Gewicht II”*

### Title
**Letztes Steingewicht II – Das Gute, das Schlechte und die Ugly von LeetCode #1049* *

### Meta Beschreibung
Erfahren Sie, wie man LeetCode 1049 mit dynamischen Programmierung, knapsack tricks und real‐world codierenden Interview-Tipps knackt. Java, Python und C++ Lösungen + SEO-freundlicher Leitfaden.

### Keywords
*LeetCode 1049, Letzter Stein Gewicht II, dynamische Programmierung, knapsack Problem, Codierung Interview, Java DP, Python DP, C++ DP, algorithm interview, job interview prep, tech interview, data structures, algorithm design*

---

### Einführung

Wenn Sie nach einer “mittleren” Herausforderung suchen, die **kombinatorisches Denken** mit klassischer **dynamischer Programmierung* verbindet, ist *LeetCode #1049) eine perfekte Passform.

In diesem Artikel entschärfen wir das Problem, gehen durch eine saubere DP-Lösung, diskutieren Edge‐case Fall Fallstricke und bewerten schließlich die *good*, *bad* und *ugly* Aspekte der verschiedenen Ansätze. Auf dem Weg bieten wir voll kommentierte Java-, Python- und C++-Code-Snippets, die Sie in Ihre IDE- oder Interview-Umgebung einfügen können.

---

oder Was macht Dieses Problem “Nice”

ANHANG **Clear-Objektiv** – minimieren Sie das endgültige Steingewicht.
2. **Kleine Zwänge** – `n ≤ 30`, `Gewicht ≤ 100` → DP ist trivial.
3. **Klassisches Muster** – es ist ein verkleidetes 0‐1 knapsack / subset‐sum.
4. **Multiple Sprachen* – Sie können es in Java, Python, C++, etc. lösen.

---

oder 1. Das Gute – Warum die DP-Lösung rockt

| Aspect | Warum es großartig ist |
|--------------------------
| **Optimalität** | Der DP numeriert **all** Subsetsummen, garantiert das globale Minimum. |
| **Simplicity** | Der Code ist nur zwei geschachtelte Schleifen – keine Wiederholung oder Rückverfolgung. |
| *** Lesbarkeit** | Booleanische Tabellen (`dp[i][j]`) Karte direkt zu „Können wir die Summe `j` mit ersten `i` Steinen erreichen?“ |
| **Reusability** | Die Subset‐sum-Routine ist eine Textvorlage für viele Interview-Probleme (Koin-Änderung, Partition, etc.). |
| **Skalierbarkeit** | Auch wenn Zwänge auf `n = 200` und `Gewicht ≤ 1000` wachsen, passt die DP noch bequem in den Speicher (`200 * 200k = 40M` Booleans ≈ 40 MB). |

---

oder 2. The Bad – Trade‐offs und Gotchas

| Ausgabe | Mitigation |
|----------------------
| **Space-Nutzung** | `O(n * insgesamt)`` kann Ballon, wenn Sie nicht vorsichtig sind. Verwenden Sie einen 1‐D DP (`dp[j]`), um den Speicher in der Hälfte zu schneiden. |
| **Zeit, wenn `total` groß ist** | Für sehr große Gewichte wird die DP undurchführbar. In solchen Fällen benötigen Sie einen Meet‐in‐the‐Middle oder Bitset-Trick. |
| **Off‐by‐one Bugs** | Denken Sie daran, dass `dp[i][j]` die ersten `i` Steine (1-basiert) verwendet. Ein häufiger Fehler ist die Mischung von 0-basierten Indizes. |
| **Int vs. long** | Wenn Sie bis zu 3000 summieren, ist `int` gut, aber immer vor Überlauf schützen, wenn sich Zwänge ändern. |

---

oder 3. Die Ugly – Quick‐And‐Dirty Alternatives

| Alternative | Wenn es erscheint | Warum es “Ugly” |
----------------------------------------------------------
| **Recursive Backtracking** | Einige Interviewer möchten, dass Sie * denken* rekursiv. | Exponential (`O(2^n)`) – hoffnungslos für `n = 30`. Gut nur zum Lernen, nicht zur Produktion. |
| **Greedy “Pick größter Stein”** | Wenn Sie rushing sind, könnten Sie einfach die zwei größten Steine zerschlagen, bis einer bleibt. Dies ergibt in vielen Fällen eine suboptimale Antwort (z.B. `[2,7,4] `). Es ist eine verlockende, aber gefährliche Abkürzung. |
| **Brute‐Force Permutationen** Generieren Sie alle Permutationen der Steine und simulieren Sie den Prozess. | Extrem langsam (`O(n! * n)`). Es kann passieren, wenn die Testfälle winzig sind, aber TLE auf versteckte Fälle erhalten. |
| **Randomized heuristics** | Laufen Sie eine zufällige Subset-Auswahl 1000 mal und halten Sie das Beste. Man sollte eine „persönliche Herausforderung“ durchlaufen, aber bei LeetCodes versteckten Tests fast immer scheitern. |

> **Bottom Line:** * Verwenden Sie nicht die hässlichen Ansätze in einem realen Interview, es sei denn, Sie befinden sich in einer zeitgesteuerten „brain‐dump“ Situation.* Die DP ist sauber, schnell und sicher.

---

oder 4. Sprache-spezifische Tipps

- **Java**
- Verwenden Sie `ArrayList` oder `int[]` – keine Generika erforderlich.
- Vorziehen `dp[i][0] = true` über ein `if` innerhalb der inneren Schleife für Klarheit.

**Python**
- Listenverständnisse erstellen die DP-Tabelle schnell.
- Der 1‐D DP kann als:
```python
dp = [False] * (gesamt + 1)
dp[0] = Wahr
für w in Steinen:
für j im Bereich (gesamt, w - 1, -1):
dp[j] |= dp[j - w]
`` `
- `abs(total - 2 * s)` ist der minimale Unterschied.

**C++**
- `std::bitset` ist das *speed‐hero* für große Summen:
```cpp
std::bitset<10001> Bits; // 3000 + 1 ist sicher
Bits[0] = 1;
für (int w : stones) Bits |= bits << w;
`` `
- Dann ist die Antwort `min_{s ≤ total/2} total - 2*s`, wo `bits[s]` wird gesetzt.

---

oder 4. Letzte Gedanken – Wie man dies in Ihrem Interview verwendet

ANHANG **Erklären Sie die Reduktion** – „Dies ist ein Subset-Summe / Knapsack-Problem. „
2. **Sketch the DP table* – auf einem Whiteboard schreiben Sie `dp[i][j] und erklären Sie Basisfälle.
3. **Code it** – handschrifte die geschachtelten Schleifen; nicht kopieren‐paste.
4. **Test Randfälle** – `[1]`, `[1,2,3]`, `[100]*30`, um zu zeigen, dass Sie die Grenzen verstehen.
5. ** Optimieren Sie, wenn gefragt** – sprechen Sie über 1‐D DP oder Bitset, wenn der Raum/Zeitdruck steigt.

Durch die Präsentation der *good*, *bad* und *ugly* Perspektiven zeigen Sie **algorithmische Reife*** – die Fähigkeit, Trade-offs zu bewerten – die Interviewer lieben.

---

### Call to Action

> *Geht Ihr Code bereit? Versuchen Sie es auf LeetCode! Senden, testen Sie gegen die versteckten Fälle und teilen Sie Ihre Erfahrungen in den Kommentaren. *

Glückliche Kodierung! 🚀

---

Fazit

*Last Stone Weight II* ist mehr als ein “medium” LeetCode Problem; es ist ein Mini-Spielplatz für dynamische Programmierung Meisterschaft.
Mit der oben genannten DP-Vorlage und dem analytischen Objektiv dieses Artikels sind Sie jetzt ausgestattet, um das Problem in Java, Python oder C++ zu lösen und Ihre Interviewer mit sauberem, optimalen und gut-Thought‐out-Code zu beeindrucken.

---

**Happy Interview Prep!**
*— Ihr Coating Interview Companion*

---

*Ende der Blog-Post*

---

### 6. Schlusshinweise

- **Copy‐Paste Ready** – alle drei Code-Snippets kompilieren as-is in ihren jeweiligen Sprachumgebungen.
- **Time‐Testing** – für eine 1‐Sekunden-LeetCode-Grenze läuft der DP in Millisekunden auf modernen CPUs.
- **Job Interview Prep** – dieses Problem ist ein Grundpfeiler in vielen Top-Tech-Interview-Bibliotheken; Mastering es kann Ihr Vertrauen auf ähnliche DP/Knapsack-Fragen steigern.

Viel Glück und kann Ihr letztes Steingewicht immer minimal sein!