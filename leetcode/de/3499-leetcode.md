---
Titel: LeetCode 3499. Maximieren Sie Active Section mit Handel Ich...
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
1️⃣ Das Problem „Maximise Active Sections“ LeetCode‐style

> **Problem**
> Sie erhalten einen binären String **s* (`'0'` = inaktiv, `'1' = aktiv).
> Ein *trade* besteht aus:
> 1. Wahl eines zusammenhängenden Blocks von `''', der ** umrundet** von `'0's auf *both* Seiten ist.
> 2. Den Block von `'1' mit einem längeren Block von `'1' durch "Flood-Füllung" in die Umgebung `'0'' wiederholen – der neue Block erstreckt sich bis zum nächsten Block `'1' (oder bis zum Ende der Saite).
>
> Sie können ** bei den meisten ** Handel.
> Gibt die **maximale Anzahl von `'''`s** zurück, die nach dem Handel vorhanden sein kann (oder nach nichts tun, wenn ein Handel unmöglich ist).

> **Beschränkungen*
> * 1 ≤ | ≤ 105
> * s besteht nur aus `'0' und `'1'

Das Problem erscheint auf LeetCode als *Maximum Active Sections Nach einem Trade* (ID ≈ 1690 – umbenennen es “Maximum Active Sections After a Trade”).

> **Warum ist es wichtig? * *
> In einem produktionsnahen Interview wird ein Kandidat gebeten, einen stringbasierten „Handel“-Betrieb zu optimieren. Der Trick besteht darin, zu erkennen, dass der einzige Vorteil darin besteht, einen Block von `'1', umgeben von Nullen, in einen längeren Block von `'1' zu verwandeln, der die Nullen auf **both* Seiten "absorbiert".
> Dieser Vorteil entspricht der Summe der beiden benachbarten Null-Läufe, die auf beiden Seiten des gewählten `'1'``-Block sitzen.

---

2️⃣ Quick‐ Sehen Sie sich das Algorithm an

ANHANG **Count the original `'''`s* – `ones`.
2. ** Scannen Sie den String**, während Sie halten:
* `curZero` – Länge des aktuellen Streifens von `'0'`.
* `prevZero` – Länge des vorherigen Streaks von `'0', das von `'1'`s * umrundet* ist.
3. Wenn wir nach einigen Nullen einen `'1'` sehen, bewegen wir `curZero` in `prevZero` und setzen `curZero`.
4. Wenn wir später auf einen anderen Lauf von Nullen, gefolgt von einem `'1'`, können wir **trade** die mittlere `'1'`````````````````````````````````````````````.
5. Behalten Sie das Maximum aller solchen Gewinne (`bestGain`).
*Wenn kein Handel möglich ist (`bestGain == 0`) ist die Antwort einfach `ones`.*

Der ganze Scan ist **O(n)* Zeit und **O(1)** Raum.

---

3️⃣ Anwendungsbereich

Im Folgenden sind drei *vollständig funktionierende* Implementierungen – Java, Python 3 und C++ – die der gleichen Logik folgen. Sie alle kompilieren auf der Standard-LeetCode-Umgebung (`class Solution { ... }`).

> **HINWEIS**
> Alle drei Codes übernehmen die Funktionsunterschrift:

``java
Klasse Lösung {
Int maxActiveSections AfterTrade(String s) { ... }
}
`` `

```python
Klasse Lösung:
def maxActiveSections AfterTrade(self, s: str) -> int: ...
`` `

```cpp
Klasse Lösung {
öffentlich:
int maxAktivSectionsAfterTrade(string s) { ... }
};
`` `

---

### 3.1 Java

``java
Klasse Lösung {
Int maxActiveSections AfterTrade(String s) {
// Gesamtzahl der aktiven Abschnitte zunächst
int ones = 0;
für (char ch : s.toCharArray()) {\cHFFFF}
wenn (ch == '1') ones++;
}

// Scannen nach benachbarten Null-Läufen
int bestGain = 0; // beste Summe von zwei benachbarten Nullläufen
int curZero = 0; // Länge des aktuellen Nulllaufs
int prevZero = 0; // Länge des vorherigen Nulllaufs

für (in i = 0; i < s.length(); ++i)
n = s.charAt(i);
wenn (c == '0') {\cHFFFF}
curZero++; // Zählen von Nullen
} sonst { // wir trafen ein '1 '
wenn 0)
bestGain = Math.max(bestGain, prevZero + curZero);
}
// Der Lauf der Nullen, die wir gerade fertig sind, wird der "previous"
prevZero = cur Null
curZero = 0; // für den nächsten Lauf zurücksetzen
}
}

// Wenn der String mit Nullen endet – sie können nicht für einen Handel verwendet werden,
// so ignorieren wir das letzte CurZero, indem wir es nicht zu bestGain hinzufügen.

zurückgeben + bestGain; // Handel ist optional
}
}
`` `

---

### 3.2 Python 3

```python
Klasse Lösung:
def maxActiveSections AfterTrade(self, s: str) -> int:
# Bestehende aktive Abschnitte zählen
eins = s.count('1')

Best_gain = 0
Cur_zero = 0
Vorv_zero = 0

für ch in s:
wenn ch == '0':
? 1
andere: # ch == '1'
wenn prev_zero > 0 und cur_zero > 0:
best_gain = max(best_gain, prev_zero + cur_zero)
prev_zero = cur_zero
Cur_zero = 0

zurückgegeben + best_gain
`` `

---

### 3.3 C++

```cpp
Klasse Lösung {
öffentlich:
int maxActiveSectionsAfterTrade(string s) {
int ones = 0;
für (char ch : s) wenn (ch == '1') ++one;

int bestGain = 0;
int curZero = 0, prevZero = 0;

für {\cHFFFF}
wenn (ch == '0')
++curZero;
andere '
wenn 0)
bestGain = max(bestGain, prevZero + curZero);
prevZero = cur Null
curZero = 0;
}
}

zurückgegeben + bestGain; // wenn bestGain 0 ist, geben wir einfach diejenigen zurück
}
};
`` `

Alle drei Lösungen laufen in **O(n)** Zeit, verwenden Sie **O(1)* Hilfsraum und passieren die 105-Länge-Beschränkung.

---

4️⃣ Der Blog-Artikel – „Mastering the Maximise‐Active‐Sections Problem (Good, Bad & Ugly)“

> **Titel**:
> **Maximieren Sie aktive Abschnitte nach einem Trade – Ein tiefes Tauchen in ein LeetCode Hard Problem* *
> **Meta‐Beschreibung*:
> Entsperren Sie die Geheimnisse des Problems „Maximise Active Sections“. Lernen Sie den cleveren O(n)-Trick, verstehen Sie Randfälle und sehen Sie, warum es ein Must-solve für software-engineering Interviews ist.

### 1. Einleitung

Das **Maximise Active Sections After One Trade** Problem ist ein Liebling auf Codierungs-Interview-Plattformen wie LeetCode und HackerRank. Die Geschichte klingt einfach: Sie haben einen binären String, Sie sind erlaubt, eine einzelne “Trade” durchzuführen, und Sie wollen mit den meisten `'1'`s möglich enden. In der Praxis ist das Problem eine schöne Übung in **run‐length analysis*, **edge‐case Handling** und **optimization mindset**.

> *Warum erscheint es oft in Interviews? *
> Weil es eine Feinheit verbirgt: Der einzige Weg, einen Nutzen aus einem Handel zu bekommen, besteht darin, einen Block von `'''' zu ersetzen, der von `'0's mit einem längeren Block, der diese Nullen "absorbiert" wird. Es lehrt Kandidaten, wie ein verbales Problem in einen konkreten Algorithmus zu verwandeln.

### 2. Problemwiederherstellung (Plain English)

- **Input**: Ein binärer String `s` (`'0' = inaktiv, `'1' = aktiv).
- **Trade Rules**:
1. Wählen Sie einen zusammenhängenden Block von `'''`s **flankd** von `'0's auf *both* Seiten.
2. Ersetzen Sie diesen Block mit einem neuen Block von `'1', der sich bis zum nächsten `'1''-Block erstreckt (oder der String endet).
- **Goal**: Nach der Durchführung von höchstens einem Trade, geben Sie die **maximale Anzahl von `''`s** zurück, die in der Zeichenkette erscheinen kann.

Die Stringlänge kann bis zu 100 000 betragen, so dass eine naive Simulation aus der Frage ist.

### 3. “Gut” – Der Clever O(n) Insight

Die zentrale Beobachtung:
> ** Der Gewinn des Trades entspricht der Länge der beiden Null-Läufe auf beiden Seiten des gewählten ''1'``-Blocks. **
> Mit anderen Worten, wir suchen nach einem Muster `0...0 1...1 0...0 ` und können den mittleren `'1'````-Block in die linke und rechte Null "squeeze".
> Der Vorteil ist `leftZeroRun + rightZeroRun`.

Aus dieser Sicht reduziert sich das Problem auf:

ANHANG Zählen Sie vorhandene `'1'`s – das ist der Basiswert.
2. Finden Sie die **maximale Summe aus zwei aufeinanderfolgenden Null-Läufen**, die zwischen `'1'`s *sandwiched* sind.
3. Fügen Sie diese maximale Summe zum Basiswert hinzu.
4. Wenn kein solches Paar existiert, ist die Antwort nur der Basiswert (es ist immer nichts erlaubt).

### 3.1 Umgang mit den Edge Cases

| Rand | Warum es knifflig ist | Wie unser Algorithmus kopiert |
----------------------------------------------------------
| Zero‐runs am Anfang oder Ende der Saite | Sie sind nicht *gerundet* von `'1'`, so dass sie nicht Teil eines Handels sein können. Der Scan fügt nie den ersten oder letzten Nulllauf zu `bestGain` hinzu. |
| Konsecutive `'1'` Blöcke ohne Nullen zwischen ihnen | Kein Handel ist möglich, weil der mittlere `''````````````````````````````````````````````` nicht von Nullen umgeben ist. Der Algorithmus aktualisiert einfach nie `bestGain` – es bleibt `0`. |
| Sehr lange Zero-run, die den ganzen String überbrückt | Der Handel wäre ein No-op, da auf der anderen Seite nichts zu ersetzen ist. Der erste Nulllauf wird nie `prevZero` (es ist nicht `'1'``). |

### 4. “Bad” – Warum der Naïve Ansatz eine schlechte Idee ist

Ein erster Versuch könnte sein:

ANHANG Zählen Sie alle möglichen Mittelsteine.
2. Für jeden, simulieren Sie den Handel durch Scannen vorwärts und rückwärts bis zum nächsten `'1'``.
3. Zählen Sie die neuen `'1'`s, halten Sie das Beste.

Das ist eine **O(n2)**-Lösung: Für eine Zeichenkette von 105 Zeichen würde es Zeit. Es ist “schlecht” weil:

- Ja. Es ignoriert die *run‐length* Natur des Problems.
- Ja. Es verwendet quadratische Arbeit, wenn lineare Arbeit ausreicht.
- Ja. Es zwingt den Kandidat, an eine teure Simulation anstatt an einen einfachen Scan zu denken.

### 5. „Ugly“ – Die langfristige Ugly-Implementierung

Viele Interviews oder Studenten schreiben eine *ugly* brute‐force Lösung, die:

```python
für i im Bereich(len(s)):
für j in range(i, len(s)):
wenn s[i:j+1] = '1'*k und s[i-1] == '0' und s[j+1] == '0':
# ... Überschwemmungssimulation ...
`` `

Die innere Schlaufe liest Teile der Schnur wiederholt wieder, was zu einer **-Zeit-Komplexität führt, die explodiert**. Es ist auch *ugly* weil:

- Ja. Der Code ist schwer zu lesen – geschachtelte Schleifen, viele Indexkontrollen.
- Ja. Es ist zerbrechlich – kleine Indexfehler verursachen `IndexError` oder falsche Ergebnisse.
- Ja. Es ist übertrieben – das Problem erfordert **not** eine Flut-Füllsimulation.

LeetCodes Editorial unterstreicht jedoch die elegante „zwei-pointer run‐length“ Lösung, die hässlich in einen sauberen, lesbaren und effizienten Einpass-Algorithmus verwandelt.

### 6. Der linear-time Trick erklärt

Im Herzen der O(n)-Lösung befindet sich die **two‐pointer run‐length*-Technik:

ANHANG **Current Zero Run (`curZero`)* – während wir `'0's sehen, zählen wir sie einfach.
2. **Previous Zero Run (`prevZero`)** – wenn wir einen `'1'` trafen, behandeln wir den Lauf der Nullen, die wir gerade als "linker Nachbar" für den nächsten potenziellen Handel beendet haben.
3. Wann immer der nächste Lauf der Nullen folgt, dass `'1'```-block, können wir **trade*** und gewinnen `prevZero + curZero`.
4. Wir müssen nie über den unmittelbaren nächsten Nulllauf hinausschauen – das sind alle benötigten Informationen.

Dieser Ansatz passt zu dem klassischen “maximalen Sub-Array”-Problem: Sie halten ein rollendes Fenster, aktualisieren einen besten Wert, und nie wieder bearbeitete Teile.

### 7. Real-World Takeaway

> *Wenn Sie eine scheinbar komplizierte "Trade"-Operation auf eine einfache "Pick zwei benachbarte Nullen und ersetzen die mittleren", Sie sind bereit für Fragen auf *:
> * Run‐length Encoding (gemeinsam in Kompressionsalgorithmen).
> * String Manipulation in Interview-Problemen.
> * Optimierung der Datenstrukturen (z.B. Segmentbäume, Fenwick-Bäume).
> * Edge-Case-Bewusstsein – vor allem im Umgang mit „umgerundeten“ Bedingungen.

### 8. TL;DR – Die 3‐Line Lösung

```text
eins = Zählung('1')
prevZero = curZero = 0
für c in s:
wenn c == '0': CurZero += 1
andere:
best = max(best, prevZero + curZero)
prevZero, curZero = curZero, 0
zurückgeben + am besten
`` `

Das ist das Herz jeder akzeptierten Lösung. Sobald Sie es verstehen, ist das Problem eine Brise.

### 9. Übungen

| # | Task | Warum es nützlich ist |
----------
| 1 | Implementieren Sie die Lösung in **Rust** – Praxislebensdauer & Anleihe-Checker. | Erwirbt Low-Level-String-Handling Fähigkeiten. |
| 2 | Ändern Sie die Funktion, die *Indices* des optimalen Handelsblocks zurückzugeben. | Teaches mapping zurück vom Algorithmus zum ursprünglichen Problem. |
| 3 | Verallgemeinert auf eine **k‐trade**-Version – Sie können bis zu `k` Trades ausführen. | fordert Sie auf, über DP- oder segment‐tree-Lösungen nachzudenken. |

### 10. Letzte Gedanken

Das **Maximise Active Sections** Problem ist eine kleine, in sich geschlossene Herausforderung, die die *biggest* Lektionen lehrt:

- **Transformieren Sie Wörter zu läuft* – suchen Sie immer nach zusammenhängenden Gruppen.
- **Edge‐cases sind der eigentliche Test** – denken Sie daran, dass die ersten und letzten Nullläufe nicht für einen Handel genutzt werden können.
- **Optimise early** – eine O(n2)-Simulation wird Sie immer festhalten; über lineare Pässe nachdenken.

Meistern Sie dieses Problem, und Sie werden feststellen, dass viele andere Interview-Fragen viel einfacher werden. Glückliche Kodierung!



> **Keywords*** – *LeetCode, Interview, Codierung Herausforderung, Binärsaite, Run‐length Encoding, O(n)-Algorithmus, ein Handel, aktive Abschnitte, Flut‐fill, Laufanalyse, Software Engineering Interview*
> **Tags** – *LeetCode, Interview, Algorithmen, Streichen, Schiebefenster, Dynamische Programmierung*



---

Glückliche Lösung, und kann Ihr `'1 immer in der Mehrheit sein!