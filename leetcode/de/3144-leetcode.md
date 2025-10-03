---
Titel: LeetCode 3144. Minimale Substring-Partition der Gleichzeichenfrequenz -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
# 3144 – Minimale Substring-Partition des Gleichen Zeichens Häufigkeit
> **LeetCode | Dynamische Programmierung | O(n2·26) | 100-Punkt-Lösung* *

---

TL;DR
Bei einem Kleinbuchstaben `s`, spalten Sie es in die wenigsten möglichen Substrings, so dass *jedes Substring ist "ausgeglichen" * - jedes Zeichen im Substring erscheint die gleiche Anzahl von Zeiten.
Wir lösen das Problem mit einem klassischen DP, der in **O(n2·26)* Zeit und **O(n)* Raum läuft.

| Sprache | Zeit | Raum |
|-------------------------
| **C++* | O(n2·26) | O(n) |
| **Java** | O(n2·26) | O(n)
| **Python** | O(n2·26) | O(n) |

---

oder 1. Problemwiederherstellung

> **Minimum Substring-Partition der Gleichzeichenfrequenz**
>
> **Input:** `s` – eine Reihe von Länge `1 ... 1000` mit nur Kleinbuchstaben.
> **Ausgang:** die minimale Anzahl der Unterstrings in einer Partition von `s`, wo jede Unterstrierung *ausgeglichen* ist.
> Ein Substring ist **balanced**, wenn alle Zeichen, die in ihm erscheinen, die gleiche Anzahl von Zeiten auftreten.

Beispiel
`` `
s = "ababcc"
gültige Partitionen: ("abab","c","c"), ("ab","abc","c"), ("abcc")
ungültige Partitionen: ("a","bab","cc"), ("aba","bc","c"), ("ab","abcc")
`` `

---

oder 2. Intuition & Strategie

* Wir betrachten den String von links nach rechts.
* Lassen Sie `dp[i]` die minimale Anzahl von ausgewogenen Substrings sein, die benötigt werden, um das Präfix `s[0 ... i] zu decken.
* Für jeden `i` schauen wir rückwärts und versuchen, ein ausgewogenes Substring an `i` zu beenden.
* Beim Verschieben des Startzeigers `j` von `i` nach unten auf `0` halten wir die Frequenz jedes Zeichens in `s[j ... i] `.
* Wenn das aktuelle Fenster ausbalanciert ist, können wir die Partition auf `i` als `dp[j-1] + 1` beenden.
* Die Antwort ist `dp[n-1]`.

Das Schiebefenster, das *Balance* prüft, ist **O(26)** pro Schritt (nur 26 Buchstaben).
Die Gesamtkomplexität ist also **O(n2·26)**.

---

oder 3. Korrekturnachweis

Wir beweisen, dass die oben beschriebene DP die optimale Partition liefert.

### Lemma 1
Für jeden Index `i` entspricht `dp[i] die Mindestanzahl an ausbalancierten Substrings, die zur Deckung des Präfixes `s[0...i] benötigt werden.

*Proof. *
Wir zeigen durch Induktion über `i`.

*Base:* `i = 0`.
Das einzige Substring ist `s[0]`.
Wenn es ausbalanciert ist (immer wahr, weil ein Zeichen einmal auftritt) `dp[0] = 1`.
Andernfalls existiert keine Partition, aber das Problem garantiert mindestens eine Partition, so dass das Lemma hält.

*Induktionsschritt:*
Angenommen, das Lemma hält für alle Indizes `< i`.
Wenn Sie `dp[i] wir untersuchen jeden möglichen Start `j` des letzten Substrings: `j ∈ [0, i] `.
Wenn `s[j...i]` ausbalanciert ist, dann der Rest des Strings `s[0...j-1]`` kann durch die Induktionshypothese optimal in `dp[j-1]` Substrings aufgeteilt werden.
Daher ist `dp[j-1] + 1` eine mögliche Partitionsgröße für Präfix `i`.
Das Minimum über alle machbar `j` gibt die optimale Größe für `i`.
So ist `dp[i]` optimal. LAND



### Lemma 2
Die Prozedur, die die Zeichenfrequenzen beim Rückwärtsscannen aufrechterhält, bestimmt, ob `s[j...i] ` ausgewogen ist.

*Proof. *
Wir halten ein Array `freq[26], wo `freq[c] ` zählt Ereignisse des Buchstabens `c` im aktuellen Fenster.
Nach dem Hinzufügen von `s[j]` recompute `minFreq` und `maxFreq` unter allen `freq[c] > 0`.
`minFreq == maxFreq` iff jede nicht-Nullfrequenz gleich dem Wert, der genau die Definition eines ausgewogenen Substrings ist. LAND



### Theorem
Der Algorithmus gibt die minimal mögliche Anzahl von ausbalancierten Substrings zurück, die den gesamten String abdecken.

*Proof. *
Durch Lemma 1 ist `dp[n-1]` optimal für den gesamten String.
Der Algorithmus gibt `dp[n-1]` aus.
Daher ist der Algorithmus korrekt. LAND



---

oder 4. Komplexitätsanalyse

**Zeit:**
* Oberschleife über `i` (`n` Iterationen).
* Innenschleife über `j` (` ≤ n` Iterationen).
* Für jeden `j` aktualisieren wir Frequenzen in **O(1)* und prüfen die Ausgewogenheit in **O(26)**.
→ `O(n2·26)` ≈ `O(n2)` für `n ≤ 1000`.

**Space:**
* `dp`-Array: `O(n)`.
* Frequenzbereich: `O(26)`.
→ `O(n)` insgesamt.



---

oder 5. Referenzumsetzungen

Unten finden Sie saubere, kommentierte und fertig-zu-pasta-Lösungen in **C++*, **Java** und **Python***.
Alle drei folgen der gleichen DP-Strategie.

---

### 5.1 C++ (GNU C++17)

```cpp
#include <bits/stdc++.h>
mit Namespace std;

Klasse Lösung {
öffentlich:
// Helfer zu testen, ob ein Fenster ausbalanciert ist
statisches Bor istBalanced(const array<int, 26>& freq) {\cHFFFF}
int mn = INT_MAX, mx = 0;
für (int f : freq)
(f ==) 0) weiter;
mn = min(mn, f),
mx = max(mx, f)
}
zurück mn == mx; // mn==mx iff alle nicht-zero Frequenzen gleich
}

Int minimumSubstringsInPartition(string s) {
int n = s.size();
vektor<int> dp(n, n); // dp[i] = minimale Substrings für Präfix [0,i]
für (int end = 0; end < n; ++end) {
array<int, 26> freq{}; // null-initialized
für (int start = end; start >= 0; --start) {
freq[s[start] - 'a']++; // Fenster nach links erweitern
wenn (isBalanced(freq)) { // Fenster [start,end] ausbalanciert ist
Int Kandidat = (Start = = = 0) ? 1 : dp[start - 1] + 1;
dp[end] = min(dp[end], Kandidat);
}
}
}
zurückgeben dp.back();
}
};
`` `

---

### 5.2 Java (Java 17)

``java
Import java.util.*;

Public class Lösung {\cHFFFF}
// Prüfen Sie, ob das aktuelle Frequenzfeld ein ausgewogenes Substring darstellt
private statische boolean isBalanced(int[] freq) {
int min = Integer.MAX_VALUE, max = 0;
für (int f : freq)
(f ==) 0) weiter;
min = Math.min(min, f);
max = Math.max(max, f);
}
zurück min == max.
}

öffentliches Mindesteinkommen SubstringsInPartition(String s) {
int n = s.length();
int[] dp = neu int[n];
Arrays.fill(dp, n); // großer Anfangswert

für (int end = 0; end < n; end++) {\cHFFFF}
int[] freq = new int[26];
für (int start = end; start >= 0; Start---) {\cHFFFF}
freq[s.charAt(start) - 'a']++;
wenn (isBalanced(freq)) {\cHFFFF}
Int cand = (start == ? 1 : dp[start - 1] + 1;
dp[end] = Math.min(dp[end], cand);
}
}
}
Rückgabe dp[n - 1];
}
}
`` `

---

### 5.3 Python 3 (3.11)

```python
aus der Einfuhr Liste

Klasse Lösung:
@staticmethod
def is_balanced(freq: List[int]) -> bool:
""Return True iff alle Nicht-Nullfrequenzen sind gleich.""
mn, mx = Keine, Keine
für f in freq:
wenn f == 0:
weiter
wenn mn nicht oder f < mn ist:
mn = f
wenn mx keine oder f > mx ist:
mx = f
zurück mn == mx

def minimumSubstringsInPartition(self, s: str) -> int:
n = len(s)
dp = [n] * n # dp[i] = min substrings for prefix [0,i]

für Ende im Bereich(n):
freq = [0] * 26
für Start im Bereich(Ende, -1, -1):
freq[ord(s[start]) - 97) += 1
wenn selbst.is_balanced(freq):
kannd = 1 bei Start = = 0 sonst dp[start - 1] + 1
dp[end] = min(dp[end], cand)

zurück dp[-1]
`` `

---

oder 6. Blog Post – „Das Gute, das Schlechte und die Ugly der Balanced‐Substring-Partitionierung“

### 6.1 Einführung

Wenn Sie ein Software-Engineering-Kandidat für Top-Tech-Interviews sind, haben Sie wahrscheinlich LeetCode gesehen **3144 – Minimale Substring-Partition der Gleichzeichenfrequenz**.
Es ist ein *medium-schwierigkeit* DP-Puzzle, das eine große Schaufenster der Problemlösungsfähigkeit ist.
Lassen Sie uns nicht erkennen, warum dieses Problem ein job‐interview gold‐mine ist, erkunden Sie die elegante DP, die es löst, und sprechen Sie über Fallstricke, die Sie hochfahren können.

> **Keywords*: LeetCode, Interview-Fragen, dynamische Programmierung, ausgewogene Substrings, Job-Interview, Software-Ingenieur, C++, Java, Python, algorithmisches Denken.

---

### 6.2 Das Gute – Was macht es zu einem großen Interview Frage

| Aspect | Warum es galt |
|------------------------------
| **Clear Constraints** | Länge ≤ 1000, nur Kleinbuchstaben – erlaubt O(n2)-Lösungen, ohne sich um Zeitlimits Sorgen zu machen. |
| **DP‐Friendly** | Die optimale Aufteilung führt natürlich zu einem eindimensionalen DP. |
| **Multiple Languages** | Solvable in C++, Java oder Python – demonstriert Sprachvielfalt. |
| **Logical Decomposition** | Sie brechen es in “ist dieses Fenster ausgeglichen?” und “ können wir eine Partition hier beenden?” – gut zum Testen von Kommunikation. |
| **Edge‐Case Rich** | Single‐Brief oder All‐same‐Buchstaben-Strings sind trivial, aber gemischte Muster (z.B. „ababcc“) drücken Sie, um die Balance richtig zu testen. |

Interviewer lieben Probleme, bei denen ein **clean, provable DP** existiert, weil es Ihnen erlaubt, Ihre Argumentation Schritt für Schritt zu erklären und sofortiges Feedback zur Richtigkeit zu erhalten.

---

### 6.3 The Bad – Common Traps und Missverständnisse

ANHANG **Maßnahmen „ausgeglichen“* *
*Sie könnten denken, dass ein Substring ausgeglichen ist, wenn *some* Zeichen sind gleich, nicht *alle*, die erscheinen. *
Die richtige Bedingung ist ** alle Nicht-Nullfrequenzen sind identisch**.

2. ** Verwendung zusätzlicher Datenstrukturen* *
*Viele Kandidaten bauen einen `Map<Character, Integer>` innerhalb der inneren Schleife. *
Während der Funktion fügt das Overhead hinzu; ein Array der Größe 26 ist schneller und einfacher zu begründen.

3. **Vergessen des Prefix DP Transition**
Die Wiederholung `dp[end] = min(dp[end], dp[start-1] + 1) ` ist unerlässlich.
Das Skipping des `dp[start-1]` Teils gibt falsche Antworten für Präfixe, die bereits mehrere ausgeglichene Substrings enthalten.

4. **Boundary Off‐By‐One**
`start == Es gibt kein linkes Präfix.
Das Vergessen, das richtig zu handhaben, führt zu negativen Indizes oder falschen Ergebnissen.

5. **Performance Understiming*
Sie könnten denken, `O(n2·26)` ist “schnell”, aber es falsch schreiben (z.B. Frequenzen von Kratzern in der inneren Schleife) wird es auf `O(n3) schieben und Zeit aus.

---

### 6.4 Die Ugly – Was in Ihrem eigenen Code zu sehen

* ** Unnötige Re‐Computing* *
Einige naive Lösungen stellen das gesamte Frequenzarray für jedes `(Start, Ende)` Paar.
Die O(26)-Prüfung ist billig, aber das Array jedes Mal wieder aufzubauen kostet O(n) und bricht den Zeitbudget.

**Wrong Balance Check* *
Ein häufiger Fehler ist, `freq.min()` und `freq.max()` über *alle* 26 Buchstaben, einschließlich Nullen zu vergleichen.
Da Nullen niedriger `min`, Sie werden falsch Flagge Fenster als unsymmetrisch.
Der Schlüssel besteht darin, Nullfrequenzen zu überspringen.

**DP Array Initialisierung* *
Das Setzen von `dp[i] auf `i+1` ist sicher, aber die Initialisierung auf `n` (String Länge) ist intuitiver.
Das Failing, um es richtig zu füllen kann stale hohe Werte lassen, die nie aktualisiert werden.

**Memory Leak in C++**
‚array<int, 26> freq{};‘ oder unter Verwendung eines rohen `int freq[26] ` das nicht jedes `end` zurückgesetzt wird, verunreinigen spätere Fenster.

---

### 6.5 Walkthrough – The Clean DP Du wirst Dein Interviewer erzählen

> *“Wir halten ein 1‐D-DP für Präfixe und gleiten ein Rückwärtsfenster, aktualisieren ein 26-Größe-Frequenzfeld. Wenn dieses Fenster ausbalanciert ist, aktualisieren wir den DP-Eintrag.“*

ANHANG **DP Definition*
`dp[i] = min Anzahl der ausbalancierten Teilstrings für das Präfix bis zu i`.
*Warum 1‐D?* Denn wir brauchen nur die optimale Partition für das vorherige Präfix – keine 2‐D-Tabellen erforderlich.

2. **Backward Scan**
Für jedes `end`, bewegen Sie `start` links, aktualisieren `freq[s[start]] `.
Überprüfung der Ausgewogenheit in O(26).

3. **Balancentest**
Verwenden Sie `min` und `max` der nicht-Nullfrequenzen.
`min == max` → ausgeglichen.

4. **Übergang**
`candidate = dp[start-1] + 1` (oder `1`, wenn Start ist 0).
Halten Sie das Minimum über alle möglichen Starts.

5. **Ergebnis**
`dp[n-1]` ist die optimale Antwort.

---

### 6.6 Übung Tipps

| Tipp | Wie Master |
|------------------------
| **Implementieren Sie alle drei Sprachen* | Zeigt Ihnen Logik in C++, Java und Python übersetzen. |
| **Write Unit Tests** | Gültig auf trivialen Strings, all‐samen Strings, wechselnden Mustern und zufälligen Strings. |
| **Erklären Während Coding** | Gehen Sie durch `dp` Updates, Frequenzwartung und ausgewogene Überprüfung – Interviewer lieben verbale Argumentation. |
| **Time Your Runs** | On LeetCode, führen Sie 5 zufällige Testfälle aus und beachten Sie die Laufzeit – sorgt dafür, dass Ihre Lösung effizient ist. |

---

### 6.7 Fazit

LeetCode 3144 ist mehr als nur ein „mittleres“ DP-Problem; es ist ein **kompaktes Schaufenster von Schlüsselinterview-Fähigkeiten*: saubere konstrate Analyse, dynamische Programmierung, sorgfältige Edge-Case-Handling und effiziente Implementierung.

Indem Sie die oben gezeigte DP beherrschen und die gemeinsamen Fallstricke verstehen, sind Sie nicht nur bereit, die Frage zu beantworten, sondern Ihre Interviewer mit klarer Logik und robustem Code zu beeindrucken.

**Happy Codierung, und können Ihre Job-Interviews so ausgeglichen wie die Substrings, die Sie Partition!**

---

### 6.8 Letzte Worte

Wenn Sie sich auf ein Software-Engineering-Interview vorbereiten, enthalten Sie LeetCode **3144** in Ihrer Praxisliste.
Die DP-Lösung ist einfach genug, um in 30 Minuten zu kodieren, aber die dahinter liegende Begründung ist tief genug, um Lob von Senior Interviewern zu verdienen.

Viel Glück und denken Sie daran: *ausgeglichene Lösungen sind oft die besten! *

---

### 7. Take-away Checkliste

ANHANG **DP auf Präfixen* – `dp[i] = min(dp[j-1] + 1) ` über alle ausgeglichenen Fenster `[j ... i] `.
2. **O(26) ausbalanciert** – vergleichen Sie min und max. Nicht-Nullfrequenzen.
3. **Watch out for zeros** – sie müssen bei der Bestimmung der Ausgewogenheit ignoriert werden.
4. **Edge Case Handling** – `start == 0` → Kandidat = 1.
5. **Language-spezifische Best Practices** – Null-Initialisierung, gebundene Überprüfung und klare Helferfunktionen.

Verwenden Sie die oben genannten Referenz-Implementierungen als Ausgangspunkt, tweak sie zu Ihrem Stil passen, und Praxis erklären den Algorithmus laut – das macht Sie zu einem herausragenden Kandidaten. 🚀

---



> **Autor:** *Ihr freundlicher Algorithm Mentor*
> **Date:** *2024‐10‐15*
> **Tags:** LeetCode, Interview Prep, dynamische Programmierung, C++, Java, Python, ausgeglichene Substrings, algorithmische Interview-Fragen.

---



### 8. Schlussbemerkungen

Ob Sie in C++, Java oder Python kodieren, die DP-Lösung oben ist ein *kanonischer* Weg, um LeetCode 3144 anzugehen.
Fühlen Sie sich frei, es anzupassen, Memoization hinzufügen oder mit Schiebefenstern experimentieren.
Viel Glück, und können Ihre ausgewogenen Substrings immer perfekt ausbalanciert werden! 🚀



---



*Vorbereitet für: Interview-bereite Ingenieure. *
*Bitte geben Sie diesen Code in Ihr Repository oder GitHub Gist ab und verweisen Sie ihn in Ihr Portfolio. *



---



#



---



[Ende der technischen Anmerkung]