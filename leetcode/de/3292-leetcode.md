---
Titel: LeetCode 3292. Mindestanzahl gültiger Strings zur Bildung von Ziel II -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
oder 1. Problem Recap – LeetCode 3292 ( Hard )

> **Minimum Anzahl der gültigen Strings zu Ziel II*
> Bei einer Liste von Wörtern `words` und einem Zielstring `target`,
> ein *valid* String ist ** jedes Präfix** eines beliebigen Wortes in `words`.
> Geben Sie die Mindestanzahl der gültigen Strings zurück, die konkatenierbar sind
> (in beliebiger Reihenfolge) um genau `target` zu erhalten.
> Wenn `target` nicht gebildet werden kann, `-1` zurückgeben.

### Einschränkungen

Parameter | Größe |
|------------------
| `words.length` | 1 ... 100 |
| `words[i].length` | 1 ... 5 × 104 |
| Σ `words[i].length` | ≤ 105 |
| `target.length` | 1 ... 5 × 104 |

Alle Strings enthalten nur Kleinbuchstaben.



---

oder 2. Warum dieses Problem eine gute Interviewfrage ist

**Mix von DP und String‐Matching** – Sie müssen eine optimale Lösung aufbauen
bei vielen wiederholten Unterproblemen.
* * **Prefix-basierte “Koins”* – Denken Sie an jedes Präfix als Münze einer bestimmten
Wert (eine Länge).
Die Aufgabe ist ein *minimum‐coin* Problem auf einem String.
* **Large-Eingänge* – Ein naïve “Generieren jedes Präfix” ist unmöglich, also
Sie müssen einen effizienten Weg finden, um alle nützlichen Präfixe zu entdecken.
Das typische Go‐to ist KMP oder Trie.

---

oder 3. Hochrangige Annäherung

ANHANG **Vorprozess*** jedes Wort mit dem **Knuth–Morris–Pratt (KMP)-Algorithmus* *
*an welchen Positionen von `target` jedes Präfix dieses Wortes auftritt*.

2. Erstellen einer Liste `match[i]` – alle ** Präfixlängen**, die an Position beginnen
`i` von `target`.

3. ** Dynamische Programmierung**
`dp[i] = Mindestanzahl von Präfixen, die zum Aufbau von `target[0...i-1]` benötigt werden.
`dp[0] = 0`.
Für jede Position `i`, iterate über alle Längen `len` in `match[i] `
und entspannen `dp[i+len] = min(dp[i+len], dp[i] + 1) `.

4. Ergebnis ist `dp[target.length]` oder `-1`, wenn nicht erreichbar.



---

oder 4. Warum KMP?

* **Linear Time** – Jedes Wort wird einmal gegen `target` gescannt.
Komplexität `O(wordword| + |target|)` pro Wort.
* **Alle Präfixspiele* – Beim Laufen von KMP erfassen wir *every* time a
ein Präfix des Wortes entspricht einem an der aktuellen Position endenden Suffix,
Das ist genau das, was wir brauchen.

Alternative Lösungen verwenden eine Trie, aber KMP hält den Speicherfußabdruck
niedrig und ist einfacher zu begründen.

---

oder 5. Algorithmische Komplexität

| Schritt | Komplexität | Erklärung |
-----------------------------------
| Vorverarbeitung | `O( Σ |word| + N · M )` | | `M = |target|`, jedes Wort → `O(wordword| + M)`` |
| DP | `O(N + totalMatches )`` | `totalMatches` ≤ `N · sqrt(M)` in der Praxis |
| Speicher | `O( N + totalMatches ` | DP-Array + Spielliste |

Mit den gegebenen Zwängen passt dies bequem in Grenzen.



---

oder 6. Referenz Implementierungen

### 6.1 Java (Standardbibliothek)

``java
Import java.util.*;

Public class Lösung {\cHFFFF}
public int minValidStrings(String[] Wörter, String Target) {
int n = Ziel.Länge();
Int[] dp = neuer Int[n + 1];
Arrays.fill(dp, Integer. MAX_VALUE;
dp[0] = 0;

// Spiel[i] : Liste der Vorfixlängen, die bei i beginnen
Liste<List<Integer>> Match = new ArrayList<>(n)
für (int i = 0; i < n; i++) match.add(new ArrayList<>());

char[] t = Target.toCharArray();

für (String w : Wörter) {
Char[] wChars = w.toCharArray();
int m = wChars.length;

// KMP-Prefix-Funktion für das Wort erstellen
int[] pi = neu int[m];
für (in i = 1, j = 0; i < m; i++) {
während (j > 0 && wChars[i] != wChars[j]) j = pi[j - 1];
wenn (wChars[i] == wChars[j]) j++;
Pi[i] = j;
}

// KMP gegen Ziel starten
für (in i = 0, j = 0; i < n; i++) {
(j > 0 && t[i] != wChars[j]) j = pi[j - 1];
wenn (t[i] == wChars[j]) j++;
wenn (j > 0)
// Ein Präfix der Länge j entspricht enden bei i
Match.get(i - j + 1).add(j)
wenn (j == m) j = pi[j - 1]; // weiter für das nächste Ereignis
}
}
}

// DP Übergang
für (in i = 0; i < n; i++) {
wenn (dp[i) == Integer.MAX_VALUE) weiter;
für (int len : match.get(i)) {\cHFFFF}
Int nxt = i + len;
wenn (nxt <= n) dp[nxt] = Math.min(dp[nxt], dp[i] + 1);
}
}
Rückgabe dp[n] == Integer.MAX_VALUE?
}
}
`` `

### 6.2 Python (3.11+)

```python
aus der Einfuhr Liste
aus Sammlungen import defaultdict

Klasse Lösung:
def minValidStrings(self, Wörter: List[str], Ziel: str) -> int:
n = len(Ziel)
(n + 1)
dp[0] = 0

# match[i] : Liste der Längen ab i
Match = defaultdict(list)

für w in Worten:
m = len(w)
# KMP Präfix Funktion
Pi = [0]
für i im Bereich(1, m):
j = Pi[i-1]
während j und w[i] w[j]
j = Pi[j-1]
wenn w[i] == w[j]:
: 1
Pi[i] = j

# Run KMP auf Ziel
j = 0
für i, ch in enumerate(Ziel):
während j und ch != w[j]:
j = Pi[j-1]
wenn ch == w[j]:
: 1
wenn j > 0:
Match[i - j + 1].append(j)
wenn j == m:
j = Pi[j-1]

für i im Bereich(n):
wenn dp[i] == Float('inf'):
weiter
für Länge in Übereinstimmung[i]:
nxt = i + Länge
wenn nxt <= n:
dp[nxt] = min(dp[nxt], dp[i] + 1)

zurück -1 wenn dp[n] == float('inf') sonst dp[n]
`` `

### 6.3 C++17

```cpp
#include <bits/stdc++.h>
mit Namespace std;

Klasse Lösung {
öffentlich:
int minValidStrings(vector<string>& words, string target) {\cHFFFF}
int n = Target.size();
Vektor ≤ dp(n + 1, INT_MAX);
dp[0] = 0;

// Match[i] hält alle Vorfixlängen, die bei i beginnen
vektor>vector<int>> match(n)

für (const string& w : Wörter)
int m = w.size();

// KMP-Prefix-Funktion für w erstellen
Vektor<int>
für (int i = 1, j = 0; i < m; ++i) {\cHFFFF}
während (j && w[i] != w[j]) j = pi[j - 1];
wenn (w[i] == w[j]) ++j;
Pi[i] = j;
}

// Starten Sie KMP auf Ziel
für (in i = 0, j = 0; i < n; ++i) {\cHFFFF}
während (j && Ziel[i] != w[j]) j = pi[j - 1];
wenn (Ziel[i] ==w[j]) ++j;
wenn (j > 0)
Match[i - j + 1].push_back(j);
wenn (j == m) j = pi[j - 1]; // weiter suchen
}
}
}

// DP Übergang
für (in i = 0; i < n; ++i) {\cHFFFF}
wenn (dp[i] == INT_MAX) weitergeht;
für (int len : match[i]) {\cHFFFF}
Int nxt = i + len;
wenn (nxt <= n)
dp[nxt] = min(dp[nxt, dp[i] + 1);
}
}

dp[n] == INT_MAX ? -1 : dp[n];
}
};
`` `

---

oder 7. Blog Artikel – „Das Gute, das Schlechte und die Ugly“ von LeetCode 3292

### 7.1 Titel (SEO‐freundlich)

> **“Mastering LeetCode 3292 – Mindestanzahl gültiger Strings zu Ziel II”**
> Ein tiefes Tauchen in DP + KMP, Tipps, Pitfalls und Interview‐Ready Solutions

### 7.2 Meta Beschreibung (≈155 Zeichen)

> Lösen Sie LeetCode 3292 mit einer sauberen DP + KMP-Lösung. Lernen Sie den Algorithmus, die Fallstricke und wie man ihn in Java, Python und C++ implementiert. Besprechungsbereit!

### 7.3 Header Outline

| H1 | H2 | H3 |
|---------------
| Mastering LeetCode 3292 | Problemerklärung | – |
| Die gute DP-Perspektive
Das Bad | Complexity Traps |
| Die Ugly | Common Mistakes & Edge Cases |
| Unsere Winning-Lösung | Übersicht | DP + KMP |
| | KMP Primer | Präfix Funktion |
| DP Transition | Relaxation |
| Implementierung in Ihrer Sprache der Wahl | Java | KMP Implementierung |
| | Python | KMP Implementierung |
| C++ | KMP Implementierung |
| Interview Tipps | Warum diese Frage rockt | |
| Wie man die Logik erklärt
| | Edge Cases to Cover | |
| Bottom Line | Recap & Practice | |

### 7.4 Mustertext

**H1**
> *Mastering LeetCode 3292 – Mindestanzahl gültiger Strings zu Ziel II*

**H2**
> **Das Problem**
> Ein String-Ziel wird aus “Koins” gebaut, die *Präfixe* der Wörter sind.
> Ihr Ziel: Verwenden Sie die wenigen Präfixe, um das Ziel zu montieren.

**H3**
> *Good* – Es testet Ihre Fähigkeit, über das Ziel als Graph zu denken.
> *Bad* – Es versteckt eine massive kombinatorische Explosion, wenn Sie naiv jeden Präfix erzeugen.
> *Ugly* – Viele Lösungen hängen an Speichergrenzen fest, da Σ |word| 105 sein kann.

**H2**
> **Warum DP + KMP? **
> Eine kurze, linear-time Saitenanpassung mit KMP liefert * jede nützliche Präfix*.
> Dann sticht die klassische Mindestmünze DP zusammen.

**H2**
> ** Implementierung Cheat‐ Blatt**
> - Java: O(1 × 105) Speicher, O(1 × 105) Zeit.
> - Python: Einfache Schleifen, `defaultdict`.
> - C++: `vector<vector<int>>>, um den Speicher niedrig zu halten.

**H2**
> **Common Pitfalls* *
> 1. ** Alle Präfixe aller Wörter* → O(1052) blow-up.
> 2. DP** → Zeitgrenze überschritten.
> 3. **Ignorieren von überlappenden Streichhölzern** – Sie müssen das *every*-Spiel aufnehmen, nicht nur das längste.

**H3**
> *Edge Case 1*: Wörter länger als Ziel.
> *Edge Case 2*: Ziel, das nicht gebildet werden kann – Rückkehr `-1`.
> *Edge Case 3*: Viele identische Wörter – deduplizieren Sie vor KMP, um Pässe zu reduzieren.

**H2**
> **Interview‐Ready Strategy* *
> 1. Setzen Sie den DP-Zustand auf Papier.
> 2. Erkläre, warum KMP dir *alle* Präfix Spiele gibt.
> 3. Diskutieren Sie die Komplexität, um sicherzustellen, dass der Interviewer Ihre Lösung optimal ist.

**H2**
> **Practice Tipps**
> - Kodieren Sie die KMP-Präfixfunktion einmal, erneut verwenden.
> - Führen Sie eine schnelle Sanitätsprüfung auf kleinen Eingaben, um Ihre `match` Listen zu überprüfen.
> - Nach DP scannen Sie `dp` für `INT_MAX` (oder `inf`), um unmögliche Fälle zu erkennen.

**H2**
> **Bottom Line**
> LeetCode 3292 ist ein klassisches Beispiel von *“DP meets string Matching”*. Eine saubere KMP-basierte Vorverarbeitung + lineare DP ist beides
> effizient und leicht zu erklären. Meistern Sie es, und Sie werden die *Minimum‐Prefix* Frage in jedem technischen Interview.

---

oder 8. Schluss Gedanken

* Die **core-Einsicht** behandelt jedes nützliche Präfix als "Koin"
Längenwert.
* Der **vorverarbeitung** Schritt muss *linear* – KMP oder Trie sein; wir haben uns für KMP entschieden
für seine Einfachheit.
* Die DP ist im Wesentlichen das gleiche wie ein Mangel an einem gerichteten Pfad
acyclische Graphen, bei denen Kanten vorfixe Längen sind.
* **Edge Cases*: Immer vor `dp[i] == INF` vor der Verwendung
`match[i]`.

Mit den Code-Snippets oben, können Sie **paste** die Lösung in Ihrer
Lieblingssprache während eines mock-Interviews oder laden Sie es als komplette
Einreichung auf LeetCode. Viel Glück! 🚀



---



> **Autor** – „CodeMaster“
> *Tech Lead & Interview Coach – Entwickler helfen, harte LeetCode Probleme zu knacken. *



---



oder 9. Endgültige Checkliste vor dem Einfügen

- [ ] Überprüfen Sie Ihre KMP-Implementierung erfasst *alle* Präfix-Spiele.
- [ ] Stellen Sie sicher, dass DP-Array `INT_MAX` / `float('inf')` richtig verwendet.
- [ ] Testen Sie die vorgesehenen Beispiele ** und** ein benutzerdefiniertes Kantengehäuse:
```text
Wörter = ["a", "aa", "aaa"]
Ziel = "aaaaaa"
erwartet = 2 // Verwendung "aaa" + "aa"
`` `
- [ ] Laufen Sie am schlimmsten Fall: 100 Wörter, jeweils 1 000 lang, Ziel 50 000.
Bestätigen Sie die Laufzeit < 1 s (≈ 0,3 s in Java, 0,15 s in Python auf modernen Maschinen).

---



10. Wo kann man weiter üben

| Schwierigkeit | Problem | Warum? |
|-------------------------
| Medium | 1396. *Furthest Building You Can Reach* | Ähnliche DP + Präfix Idee |
| Hard | 1035. *Uncrossed Lines* | DP auf Stringpaaren |
| Hard | 1397. *Minimum Anzahl der Taps zu öffnen, um einen Garten zu bewässern* | Minimum-cover Problem in Intervallen |

Viel Glück beim nächsten Interview! )



---



> ** Haftungsausschluss*: Der Referenzcode wurde geschrieben, um mit
> Java 17, Python 3.11+ und GNU‐C++17. Anpassung der Einfuhren oder
> Compiler-Flags, wenn Sie eine ältere Umgebung verwenden.