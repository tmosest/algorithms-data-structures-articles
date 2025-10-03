---
Titel: LeetCode 3597. Partition String -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
# Mastering LeetCode 3597 – **Partition String**
*Java • Python • C++ Lösungen – Das Gute, das Schlechte und die Ugly (SEO‐Optimiert)*

---

oder Warum dieses Problem Ihre Resume

- **Hard‐er als es aussieht** – ein klassischer gieriger Trick, der als „einzigartiges Substring“-Puzzle verkleidet ist.
- **LeetCode #3597* – erscheint in vielen Interviewsets auf mittlerer Ebene (Google, Amazon, Microsoft).
- **Sprachen** – Sie sehen die gleiche Logik, die in Java, Python und C++ implementiert ist – perfekt, um Cross-Paltform-Mastery zu präsentieren.
- **Zeit & Raum** – O(n) Zeit & O(n) Raum – sauber, skalierbar und „produktionsbereit“.

Wenn Sie das nageln, werden Sie zeigen:

ANHANG **Greedy Strategie** – die Auswahl des kürzesten einzigartigen Segments.
2. **Datenstrukturintuition* – Hash‐Sets gegen Karten.
3. **Kleiner Code** – präzise, lesbar und fehlerfrei.

---

Probleme der Wiederherstellung

> Bei einem String `s` von Kleinbuchstaben, Partition `s` in **unique* Substrings.
>
> Beginnend vom Index `0`, verlängern Sie den aktuellen Substring, bis er *neu* wird (ist noch nie als Ganzes erschienen).
> Wenn das Substring einmalig ist, fügen Sie es in die Antwortliste, markieren Sie es als “seen”, und starten Sie die nächste Substring aus dem nächsten Zeichen.
>
> Geben Sie die Liste der Substrings in der Reihenfolge zurück, die sie erstellt wurden.

> **Beschränkungen*
> `1 <= s.Länge <= 105 `
> `s` enthält nur Kleinbuchstaben.

---

Intuition – “Das Greedy Shortest‐Unique” Prinzip

Denken Sie an die Saite als Förderband von Briefen.
Wenn Sie ein Segment bauen, müssen Sie ** nicht überschreien** der erste Punkt, an dem das Segment *neu* wird.
Wenn Sie über diesen Punkt hinausgehen, verschwenden Sie Zeit und erstellen Sie eine längere Unterzeichnung, die vorher geteilt worden wäre.

So ist der optimale Algorithmus:

ANHANG Starten Sie ein Segment am aktuellen Index.
2. Behalten Sie die Zeichen, bis das Segment nicht im `seen`-Set ist.
3. Fügen Sie dieses Segment an das Ergebnis an, `seen` hinzu und starten Sie ein neues Segment am nächsten Index.

Dies läuft in linearer Zeit, da jedes Zeichen genau einmal verarbeitet wird.

---

~ Edge‐ ~ Fall “Die Ugly”

| Fall | Warum es bricht Naïve Ansätze |
---------------------------------------------
| `aaaaa...` (alles gleiche) | Eine naive geschachtelte Schleife kann wiederholt das gleiche Präfix testen, wodurch O(n2). |
| `abcabcabc...` | Die gierige Regel sorgt dafür, dass wir niemals `abcabc` bauen; einige Implementierungen erlauben jedoch irrtümlich überlappende Wiederholungen. |
| Sehr lange Eingabe (105) | Mit einem `StringBuilder`, der Substrings jedes Mal kopiert, kann Speicher/Zeit aufblasen. |

Der Schlüssel besteht darin, ein *hash‐set* zu verwenden, das das Substring in O(1) überprüft und das aktuelle Segment inkremental baut.

---

In den Warenkorb

### 1. Java

``java
Import java.util.*;

Klasse Lösung {
Public List<String> PartitionString(String s) {
int n = s.length();
List<String> ans = new ArrayList<>();
Set<String> gesehen = neu HashSet>>;

StringBuilder cur = new StringBuilder();
für (in i = 0; i < n; i++) {
cur.append(s.charAt(i));
wenn (!seen.contains(cur.toString()))) {\cHFFFF}
ans.add(cur.toString());
(cur.toString());
cur.setLength(0); // Zurücksetzen für das nächste Segment
}
}
Rückgabe ans;
}
}
`` `

- **Zeit**: `O(n)` – jedes Zeichen hat einmal angehängt.
- **Space**: `O(n)` – Ergebnis + Satz.

---

### 2. Python 3

```python
aus der Einfuhr Liste

Klasse Lösung:
def PartitionString(self, s: str) -> Liste[str]:
siehe = set()
as = [
= []
für ch in s:
cur.append(ch)
seg = ''.join(cur)
wenn nicht gesehen:
ans.append(seg)
siehe.add(seg)
cur.clear()
Rückgabe an
`` `

Python's `''.join()` auf einer wachsenden Liste ist `O(len(cur)) `, aber insgesamt noch linear, weil jeder Wagen genau einmal verbunden ist.

---

### C++

```cpp
#include <bits/stdc++.h>
mit Namespace std;

Klasse Lösung {
öffentlich:
vektor<string> Partition String (String s) {
unordered_set<string> gesehen;
vektor<string> an;
String Cur;

für (char c : s) {\cHFFFF}
cur.push_back(c)
wenn (!seen.count(cur)) {
ans.push_back(cur);
gesehen.insert(cur);
cur.clear();
}
}
Rückgabe ans;
}
};
`` `

- **unordered_set** gibt `O(1)` Lookup.
- `cur.clear()` hält den String klein – keine unnötigen Kopien.

---

(Optional)

```python
wenn __name__== "__main__":
sol = Lösung()
Prüfungen = [
"abbccccd", ["a","b","bc","c","cc","d"]),
"abcabcabc", ["a","b","c","ab","ca","bc"]),
("aaaaaaaaaaa", "a", "aaaaa", "aaaaaaa", "aaaaaaaaaa"]),
("xyz", ["x","y","z")
!
für inp, exp in Tests:
out = sol.partitionString(inp)
behaupten == exp, f"FAIL: {inp} → {out} (erwartet {exp})"
print("Alle Tests bestanden!")
`` `

---

Gut, Bad, Ugly – Welche Interviewer suchen

**Good*********************
------------------------
| ***Greedy Proof** – keine Rückverfolgung, einfache Logik. | **Hash‐set missuse** – mit einem `List`, um gesehene Substrings zu verfolgen → `O(n2)`. | **String copying*** – Erstellen einer neuen Zeichenkette kann TLE auf 105 Länge verursachen. |
| **Space‐effizient** – Speichern Sie nur gesehene Segmente, nicht alle Präfixe. | **Excessive Memory** – Vorverlagerung von riesigen Arrays oder `StringBuilder` Kopien. | **Recursive Lösung** – Stack-Überlauf für lange Eingänge. |
| **Cross-lang Klarheit** – identischer Algorithmus in Java, Python, C++. | **Implizite Annahmen** – z.B., dass die Eingabe nur Kleinbuchstaben enthält. **Keine Fehlerbehandlung** – stumm auf leeren Strings (obwohl Einschränkungen es verbieten). |

---

Gesprächspunkte

ANHANG **Greedy Beweis** – Zeigen Sie, warum das „kurteste einzigartige Segment“ optimal ist.
2. **Datenstrukturwahl** – Hash‐set vs. trie vs. map – diskutieren Time trade‐offs.
3. **Komplexität** – Emphasise `O(n)` – wichtig für 105-Länge-Strings.
4. **Testing** – Erwähnung von Grenzfällen (alles gleiches Schreiben, alternierende Muster).
5. **Postielle Fallstricke* – Erwähnt der Interviewer „Überlaps erlaubt?“, klären Sie, dass Wiederholungen ganze Unterstriche sein müssen.

---

SEO Meta (für die Blog-Plattform)

- **Titel**: „Java, Python, C++ – Partition String LeetCode 3597 – Interview‐Ready Solution“
- **Beschreibung**: „Step‐by-Schritt-Anleitung zu LeetCode 3597 – Partition String. Lernen Sie die gierige Strategie, Randfälle und erhalten Sie saubere Java-, Python- und C++-Code für Interviews. „
- **Keywords*: *LeetCode Partition String*, *Java-Lösung*, *Python-Lösung*, *C++-Lösung*, *Greedy algorithm*, *Hash‐set*, *Interview problem*, *Resume Boost*, *Coding interview*.

---

Letzte Gedanken

Partition String ist ein **tiny Edelstein** in der LeetCode Toolbox.
Mit einem einzigen gierigen Pass und einem Hash-Set können Sie es in linearer Zeit lösen, unabhängig von der Eingabegröße.

**Good** – Reine gierige Logik, O(n) Komplexität.
**Bad** – Über- oder Nestschleifen, die zu O(n2) führen.
**Ugly** – Speichermissbrauch oder unsachgemäße String-Konstruktion, die TLE auf großen Daten verursacht.

Das Mastering dieses Problems zeigt, dass Sie * einen präzisen Algorithmus in mehrere Sprachen * übersetzen können, ein Trait jeder Senior Engineer Rekrutierer sucht nach. Glückliche Kodierung – und viel Glück bei Ihrem nächsten Interview!