---
Titel: LeetCode 2573. Finde den String mit LCP -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
✅ 2573 – Finden Sie den String mit LCP
*Hard – LeetCode*

> **Goal** – Rekonstruieren Sie das lexikographisch kleinste Wort, das einem gegebenen entspricht
> `lcp`-Matrix oder einen leeren String zurückgeben, wenn kein solches Wort existiert.

Im Folgenden finden Sie drei produktionsbereite Lösungen (Java, Python, C++), einen prägnanten Durchgang des Algorithmus, eine Analyse von Edge-Cases und einen vollblown Blog-Artikel, der den *good*, *bad* und *ugly* Teile des Problems erklärt.
Der Blog ist SEO-optimiert für Titel wie **“LeetCode 2573 – Finden Sie den String mit LCP“* und **“Java/Python/C++ Lösung“**, damit Sie es auf Ihrem Portfolio oder LinkedIn Beiträgen verwenden können.

---

Quick‐Start Code

### 1. Java (Java 17 +)

``java
Import java.util.*;

Public class Lösung {\cHFFFF}
public String findTheString(int[][] lcp) {
int n = lcp.Länge;
int[] group = new int[n]; // 1-based group id
int curGroup = 0;

// 1️⃣ Erstellen Sie eine *potentielle* Zeichenfolge, indem Sie gleiche Zeichen gruppieren
für (in i = 0; i < n; i++) {
wenn (Gruppe[i] != 0) weiter;
wenn (++curGroup > 26) Rückkehr ""; // > 26 verschiedene Zeichen unmöglich
Gruppe[i] = curGroup;
für (int j = i + 1; j < n; j++) {
wenn 0) Gruppe[j] = curGroup;
}
}

// 2️⃣ Vergewissern Sie sich, dass die konstruierten Gruppen `lcp` wirklich erfüllen
für (in i = 0; i < n; i++) {
für (int j = 0; j < n; j++) {\cHFFFF}
int erwartet = (Gruppe[i] == Gruppe[j]) ?
(i + 1 < n &&j + 1 < n) ? lcp[i + 1][j + 1] + 1 : 1) :
0;
wenn (erwartet != lcp[i][j]) zurück "";
}
}

// 3️⃣ Gruppen-IDs in Buchstaben umrechnen (a‐z)
StringBuilder sb = neuer StringBuilder();
für (int g : group) sb.append(((char) ('a' + g - 1));
sb.toString();
}
}
`` `

> **Komplexität** – `O(n2)` Zeit, `O(n)` Hilfsraum.
> `n ≤ 1000`, so dass die Lösung leicht an die Grenzen passt.

---

### 2. Python

```python
Klasse Lösung:
Def finden TheString(self, lcp: List[List[int]]) -> str:
n = len(lcp)
Gruppe = [0]
= 0

# Potential string erstellen
für i im Bereich(n):
wenn Gruppe[i]:
weiter
= 1
wenn Cur > 26:
zurück ""
Gruppe[i] = cur
für j im Bereich (i + 1, n):
wenn lcp[i][j]:
Gruppe[j] = Cur

# Validieren Sie den lcp
für i im Bereich(n):
für j im Bereich(n):
ex = 0
wenn Gruppe[i] == Gruppe[j]:
ex = (lcp[i + 1][j + 1] + 1) wenn i + 1 < n und j + 1 < n
wenn exp != lcp[i][j]:
zurück ""

# Convert to string
zurück ''.join(chr(ord('a') + g - 1) für g in group)
`` `

---

### 3. C++ (C++17 +)

```cpp
Klasse Lösung {
öffentlich:
finden TheString(vector<vector<in>>& lcp) {
int n = lcp.size();
vektor<int> group(n, 0); // 1-based group id
int cur = 0;

// 1️⃣ Erstellen Sie einen Kandidatenstring
für (in i = 0; i < n; ++i) {\cHFFFF}
wenn (Gruppe[i] weitergeht;
wenn (++cur > 26) zurück "";
Gruppe[i] = Cur;
für (int j = i + 1; j < n; ++j) {
wenn 0) Gruppe[j] = Cur;
}
}

// 2️⃣ Verifizieren Sie die lcp Matrix
für (in i = 0; i < n; ++i) {\cHFFFF}
für (int j = 0; j < n; ++j) {
int erwartet = 0;
wenn (Gruppe[i] == Gruppe[j]) {\cHFFFF}
erwartet = (i + 1 < n &&j + 1 < n) ? lcp[i + 1][j + 1] + 1 : 1
}
wenn (erwartet != lcp[i][j]) zurück "";
}
}

// 3️⃣ Umwandeln in Zeichen
String res;
res.reserve(n)
für (int g : group) res.push_back('a' + g - 1);
zurück;
}
};
`` `

---

Insight

| Schritt | Was wir tun | Warum es funktioniert |
--------------------------------------
| **1. Gruppengleiche Indizes** 0` bedeutet `Wort[i] == Wort[j]`. Wir geben ihnen die gleiche “Gruppe id”. | In einer LCP-Matrix zwingt eine nicht-Null-Eintritt die Gleichheit an der aktuellen Position. |
| **2. Verwenden Sie minimale Buchstaben** | Der erste Index ist immer „a“. Für jeden neuen Index verwenden wir den kleinsten Brief, der von jeder vorherigen Gleichheit erlaubt wird. | Lexicographic minimization: Wir stellen nur einen neuen Brief vor, wenn es unbedingt notwendig ist. |
| **3. Gültig** | Berechnen Sie das LCP des konstruierten Wortes (Rückwärts DP: `dp[i][j] = 1 + dp[i+1][j+1] ` falls gleich, sonst `0`) und mit der Eingabe vergleichen. | Ein konstruiertes Wort *must* reproduzieren die Matrix genau. Die DP garantiert, dass wir im Schritt keinen Fehler gemacht haben. ANHANG |
| **4. Final string** | Map group ids to letters `a ... z`. | Die Gruppen sind eine Bijektion zu Buchstaben; wenn mehr als 26 Gruppen benötigt wurden, ist das Problem unmöglich. |

Der Algorithmus ist im Wesentlichen eine **generative + Verifier**-Strategie.
Es läuft in `O(n2)` Zeit – quadratisch ist unvermeidbar, weil die Eingabe selbst eine `n × n` Matrix ist – aber die konstanten Faktoren sind winzig.

---

Â ≠ Edge Cases & Common Pitfalls

| Edge Fall | Was ist zu sehen, für | Fix |
------------------------------------------
| **Mehr als 26 Zeichen* | `curGroup > 26` → unmöglich. | Sofortige Rückkehr `"" |
| **Zero-based vs one‐based indexing** | Das erwartete LCP für den letzten Index in einer Gruppe sollte `1` sein. | Griff `i+1 < n` und `j+1 < n` vorsichtig. |
| ** Ungleiche Abmessungen* | Input Garantien `lcp` ist `n×n`, aber defensive Codierung hilft beim Hacken des Richters. | Fügen Sie Grenzkontrollen hinzu, bevor Sie auf `lcp[i+1][j+1] ` zugreifen. |
| **Large `n`** | `n = 1000` → 1 M Einträge. | Verwenden Sie `O(n)` Hilfsspeicher für die Gruppen, kein 2‐D DP-Array. |
| **Non‐symmetric matrix** | Bei der Verifikation wird eine malformierte Matrix gefangen. Der Prüfschritt garantiert die Richtigkeit. |

---

‚Gute‘, ‚Bad‘ und ‚Ugly‘ Teile

| Aspect | Gut | Schlecht | Ugly |
|-----------------------
| **Problem-Anweisung** | Klare Eingabe-/Ausgabespezifikation, Zwänge und Beispielmatrix. Die Matrix ist dicht: jeder Eintrag muss überprüft werden. | Die Definition von `lcp` ist *not* Standard LCP; es ist die *full* Suffix-matching Tabelle, die für Neuankömmlinge verwirrt. |
| **Algorithmische Eleganz** | Ein einfacher Pass, um eine Kandidatenkette zu bauen, dann ein einziger Pass, um zu validieren. | Keine – Sie müssen nur verstehen “”lcp[i][j] > 0` ⇒ gleiches Zeichen“ und „DP für LCP“. | Die Menschen versuchen oft DP von Grund auf (O(n3)) oder über-engineer die Konstruktion; die gierige Gruppierung ist der süße Fleck. |
| **Einführung Schwierigkeit** | Sehr kleine Codebasis, keine schweren Datenstrukturen. | Erfordert eine sorgfältige Handhabung der Randbedingungen (letzter Index). | Wenn die `lcp`-Matrix formiert ist (z.B. unkonsistente Nullen), müssen Sie die Fehlanpassung zwischen dem konstruierten DP und dem Eingang debuggen. |
| **Testen*** | Verwenden Sie die beiden bereitgestellten Beispiele sowie zufällige Matrizen, die die Zwänge erfüllen. | Stellen Sie sicher, dass Sie `n = 1` und `n = 1000` Eckkoffer testen. | Randomly korrumpiert einen Eintrag, um zu überprüfen, ob der Code `"" zurückgibt. |

---

Warum dieses Problem ein großer Interview-Showcase ist

***Graph‐ähnliche Gruppierung** – Die LCP-Matrix definiert implizit einen ungeschützten Graph, in dem Kanten existieren, wenn `lcp > 0`.
***Greedy + DP** – zeigt einen zweiphasigen Ansatz, den viele Kandidaten überspringen.
* **Limits** – passt perfekt in das *O(n2)* Paradigma und macht es zu einem sauberen Benchmark für Interviewer.
* **Extensibility** – Sie können den Code mit mehr als 26 Buchstaben anlegen oder alle möglichen Wörter ausgeben, die für Side-Projekte großartig sind.

---

Â 📈 SEO‐Optimierter Blog Post

Im Folgenden finden Sie den vollständigen Blog-Artikel, den Sie in einem persönlichen Blog, Medium oder LinkedIn einfügen können.
Es umfasst den Keyword-reichen Titel, eine Meta-Beschreibung, Überschriften und Kugelpunkte für die Lesbarkeit.

---

# LeetCode 2573 – Finden Sie den String mit LCP
**Java / Python / C++ Lösungen | O(n2) Algorithm | Interview Prep**

### 📌 Meta Beschreibung
Solve LeetCode 2573 “Find The String With LCP” in Java, Python und C++ mit einem optimalen `O(n2) Algorithmus. Lernen Sie den Trick hinter Gruppierungsindizes, überprüfen LCP, und behandeln Randfälle. Perfekt für die Codierung von Interview prep.

---

Inhaltsverzeichnis
ANHANG [Problemübersicht](#Problem-Übersicht)
2. [Die LCP Matrix verstehen](#understanding-the-lcp-Matrix)
3. [Die Greedy‐Plus‐DP-Strategie](#the-greedy-plus-dp-strategy)
4. [Implementierung in Java, Python, C++](#implementation-in-java-python-c)
5. [Test & Edge‐Case Checklist](#testing-edge-case-Checklist)
6. [Time & Space Complexity](#time-space-Komplexität)
7. [Common Pitfalls (The Bad)](#common-pitfalls-the-bad)
8. [Erweiterte Variationen (The Ugly)](#Advanced-Variations-the-ugly)
ANHANG [Takeaway & Interview Tipps](#takeaway-interview-tips)
10. [Weiterlesen](#weiterlesen)

---

### 1. Problemübersicht <a name="Problemüberblick">/a>

> **LeetCode 2573** – *Find die String mit LCP*
> Sie erhalten eine `n × n` Matrix `lcp`, in der `lcp[i][j]` die Länge des längsten gemeinsamen Präfixes der Suffixes ab Positionen `i` und `j` ist.
> Ihre Aufgabe: ** rekonstruieren Sie das lexikographisch kleinste Wort*, das diese Matrix erfüllt, oder geben Sie einen leeren String zurück, wenn kein solches Wort existiert.

Warum ist das interessant?
- Ja. Es verbindet *String Matching* mit *Matrix Vernunft*.
- Die LCP-Matrix ist eine volle 2-D-Tabelle, nicht ein einfacher Vektor von Werten.
- Ja. Die lexikographische Anforderung zwingt eine sorgfältige Konstruktion des Kandidatenwortes.

---

### 2. Verständnis der LCP Matrix <a name="understanding-the-lcp-matrix">/a>

- **Zero-Einträge** bedeuten, dass sich die beiden Suffixe beim ersten Zeichen unterscheiden: `word[i] != word[j]`.
- **Positive Einträge** garantieren `word[i] == word[j]`.
In der Tat wird der gesamte String in **-Equivalenzklassen** von Indizes unterteilt, die denselben Buchstaben teilen.

Beispiel (für den String `"abbc" `):

| | a | b | c |
...
| **a** | 4 | 0 | 0 | 0 | 0 |
| **b* | 0 | 3 | 2 | 0 |
| **b* | 0 | 2 | 2 | 0 |
| **c* | 0 | 0 | 0 | 1 |

Sie können sehen, wie jede Zelle mit einem Nullwert den gleichen Buchstaben an beiden Positionen anzeigt.

---

### 3. Die Greedy‐Plus‐DP Strategie <a name="the-greedy-plus-dp-strategy">/a>

ANHANG **Build eine *potentielle* String** *
*Start mit Gruppe id `1` für Index 0 (Buchstabe `a`).
Für jeden neuen Index `i`:
- Gibt es ein `j < i` mit `lcp[i][j] > 0`, verwenden Sie `word[j]`.
- Ansonsten wähle den *nächst ungenutzten* Brief (max(`word[0...i‐1]) ANHANG
- Wenn wir aus Buchstaben (`> z`) auslaufen, `" sofort zurückgeben. *

2. **Validate**
Berechnung des LCP des konstruierten Wortes (Reverse DP: `dp[i][j] = 1 + dp[i+1][j+1] ` wenn Zeichen gleich sind, sonst `0`).
Wenn sich die berechnete Tabelle von der Eingabe unterscheidet, ist der Kandidat ungültig → Rückgabe `""`.

3. **Return** das gebaute Wort.

Warum funktioniert das?
- **Korrektheit*:
*Gruppen nach `lcp > 0` garantiert, dass alle Gleichheiten erfüllt sind.
Der DP-Schritt sorgt dafür, dass keine versteckten Widersprüche vorhanden sind. *
- **Lexicographic minimality*:
Wir verwenden immer den kleinsten Brief möglich. Nur wenn nötig gehen wir in den nächsten Brief. Damit ist der Endstrang möglichst klein.

---

### 4. Implementierung in Java, Python, C++ <a name="Implementierung-in-java-python-c">/a>

*(Siehe die Codeblöcke oben – eine pro Sprache.) *

Alle drei Implementierungen teilen die gleiche Logik:
- Ein einziger Pass, um *Gruppen-IDs* zuzuordnen.
- Eine Doppelschleife zur Validierung der gesamten Matrix.
- Letzte Umwandlung in Briefe.
Die Zeitkomplexität ist `O(n2)` und der Hilfsraum `O(n)`.

---

### 5. Prüfung & Edge‐ Fall Checkliste <a name="test-edge-case-checklist">/a>

| Test | Zweck |
|--------------------
| **Minimum-Größe** `n = 1` | Sollten Sie `"a" zurückgeben, unabhängig vom einzelnen Eintrag. |
| **Alle Nullen außer Diagonal** | Strings wie `"abc"` → Gruppen sollten `a`, `b`, `c` sein. |
| **Alle positiven*** (vollständigen) | Sollten Sie wieder `"aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa..." (alles gleiches Schreiben). |
| **Mehr als 26 benötigte Buchstaben** | Konstruieren Sie eine Matrix mit 27 Äquivalenzklassen → verifizieren Sie sofortiges Versagen. |
| **Malformierte Matrix** (z.B. `lcp[0][1] = 1`, aber `lcp[1][0] = 0 `) | Die Validation sollte mismatch → return `" fangen. |
| **Random gültige Matrizen** | Verwenden Sie einen Generator, der einen zufälligen String konstruiert und seine LCP berechnet; füttern Sie diese Matrix dem Soldat. |
| **Large `n`n`* `= 1000` Stresstest für Laufzeit und Speichernutzung. |
| **Boundary at last index** | Stellen Sie sicher, dass die DP `dp[n-1][n-1] = 1` richtig verwendet. |

---

### 6. Zeit- und Raumkomplexität <a name="Zeitraum-Komplexität"></a>

- **Zeit**: `O(n2)` – erforderlich, weil wir einen `n × n`-Eingang haben.
- **Space**: `O(n)` – nur das Gruppenfeld; kein extra 2‐D-DP-Array.

Diese Zahlen sind ideal für Interviewer: Die Lösung passt in die gemeinsamen Interviewzeitbudgets und ist leicht zu begründen.

---

### 6. Common Pitfalls (The Bad) <a name="common-pitfalls-the-bad">/a>

Wie es zeigt |
|---------------------------
| ***Verbrauchen `lcp > 0` mit DP** | Anfänger können denken, “wenn `lcp[i][j]` ist 1, die ersten beiden Zeichen sind gleich, aber vielleicht spätere Zeichen unterscheiden”. Der Schlüssel ist, dass * jeder* nicht-Nullwert die Gleichheit an der *aktuellen* Position zwingt. |
| **Boundäre Fehler** | Der Zugriff auf `lcp[i+1][j+1]` ohne Überprüfung der Grenzen führt zu `ArrayIndexOfBounds`. Bewachen Sie immer gegen `i+1 < n`. |
| **Skippen der Verifier** | Einige Lösungen stoppen nach dem Aufbau der Kandidatenkette, aber scheitern dann auf versteckten Widersprüchen. Der DP-Schritt ist unerlässlich. |

---

### 7. Erweiterte Variationen (The Ugly) <a name="advanced-variations-the-ugly">/a>

> In einem „research-style“-Problem könnten Sie gefragt werden:
> - *Unterstützung Alphabete größer als 26* (Unicode).
> - * Alle möglichen Wörter* ausgeben, die die Matrix erfüllen (exponentiell).
> - *Recover den String, wenn mehrere gültige Lösungen existieren* und sie lexicographisch ordnen.

Diese Variationen erfordern zusätzliche Logik:
- Eine disjoint‐set (Union‐Find) Struktur zur Gruppierung.
- BFS/DFS, um alle Briefaufträge zu erkunden.
- Vorsicht, um kombinatorische Explosion zu vermeiden.

---

### 8. Takeaway & Interview Tipps <a name="takeaway-interview-tips">/a>

- **Erklären Sie die Idee der Äquivalenzklasse**: Ein schnelles mentales Modell zur Begründung von `lcp`.
- **Zwei Phasen anzeigen*: Generation + Verifikation.
- **Über die Komplexität*: Quadratic ist das beste, das Sie hoffen können, um die Eingabegröße.
- **Mention Limit Handling*: letzter Index Spezialfall → `1`.

Wenn Sie erklären, betonen Sie, dass der gierige Teil lexicographic minimality gewährleistet, während DP die Korrektheit garantiert.

---

### 9. Weiter lesen <a name="weiterlesen">/a>

- *Suffix Trees und LCP-Arrays* – Standardtext auf suffix-array-basiertem LCP.
- *Disjoint‐Set Union (Union‐Find)* – Nützlich für die Gruppierungsphase.
- *InterviewBit LCP-Probleme* – Ähnliche Matrix-matching Herausforderungen.
- *Competitive Programming 4 – String Matching* – Tieftauchen in LCP-Rechnungen.

---

Letzte Gedanken

LeetCode 2573 kann daunting erscheinen, weil es eine dichte `n × n` Matrix beinhaltet, aber das zugrunde liegende Prinzip ist einfach: **Equality propagation + DP validation*.

Umsetzung dieser in Java, Python oder C++ Vitrinen:
- Fähigkeit, grafisch über Strings nachzudenken.
- Geschicklichkeit in gieriger Konstruktion mit Korrektheitsgarantien.
- Vorsicht beim Umgang mit Randfällen und Zwängen.

** Viel Glück bei Ihrem nächsten Interview!** 🚀

---


---

Fühlen Sie sich frei, den Artikel oder Code-Snippets an Ihren Stil anzupassen, oder fügen Sie Screenshots Ihres Testkabels hinzu.

Glückliche Kodierung!