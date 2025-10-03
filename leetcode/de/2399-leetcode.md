---
Titel: LeetCode 2399. Überprüfe Entfernungen Zwischen den gleichen Buchstaben -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
🚀 LeetCode 2399 – Prüfstrecken Zwischen denselben Buchstaben
> **“Das Gute, das Schlechte und die Ugly” – ein praktischer Leitfaden für gesprächsbereite Kandidaten* *

---

### TL;DR

- **Problem**: Jeder Kleinbuchstaben erscheint **genau zweimal** in einem String `s`.
Für jeden Buchstaben `i` (`'a' → 0`, ..., `z' → 25`) das Array `distanz[i] sagt, wie viele **andere* Buchstaben zwischen seinen beiden Vorkommen liegen sollten.
Return `true`, wenn `s` alle angegebenen Entfernungen erfüllt.

- **Lösung**:
1. **Track‐First** – Speichern Sie den ersten Index jedes Buchstabens und bestätigen Sie dann auf dem zweiten Auftritt.
2. **Check‐Second* – Wenn Sie einen Brief sehen, schauen Sie sofort vor `entfernung + 1` Schritte und vergleichen; setzen Sie den Eintrag zu `-1`, um Doppelprüfung zu vermeiden.

- **Komplexität*
- Zeit: `O(|s|)` (≤ 52)
- Raum: `O(26)` (constant)

- **Warum ist es wichtig*:
Das Muster ist in string‐and‐array Interviewfragen üblich. Das Mastering zeigt, dass Sie mit * Zwei-Pass*-Logik, Kartennutzung und Kanten-Fall-Sicherheit umgehen können.

---

1️⃣ Problem Recap

```text
Eingang
----
s – String (Länge 2‐52, alle Kleinen)
Distanz – int[26] (0‐basiert für 'a'...'z')

Ausgangsleistung
----
boolean – true iff s ist ein “well‐spaced” String
`` `

*Beispiel*

`` `
s = "abaccb"
Abstand = [1,3,0,5,0...] // nur a,b,c Materie
Ergebnis: true
`` `

---

2️⃣ Zwei gewinnende Ansätze

| Ansatz | Idea | Pros | Cons |
|------------------------
| **Track‐First*** | Remember first index; on second index compute `i - firstIndex - 1`. | Einfach, klar. | Erfordert ein „first‐seen“-Flag; verwendet ein Array von 26 Ints. |
| **Check‐Second** Beim ersten Auftreten direkt peek `i + Abstand + 1 `. Mark wie verarbeitet (`-1`). | One‐pass; keine Notwendigkeit für separate Flag-Array. | Leicht schwieriger zu verstehen; verwendet `Abstand`-Array mutierbar. |

Im Folgenden finden Sie **Java, Python und C++**-Implementierungen für *both*-Methoden, so dass Sie diejenige auswählen können, die Ihren Stil passt.

---

3️⃣ Code Snippets

> **Tip:*** Alle Lösungen gehen davon aus, dass die Zwänge garantieren, dass jeder Brief erscheint *genau zweimal*, so dass keine zusätzliche Validierung über die Grenzen hinaus erforderlich ist.

### 3.1 Java

``java
// ---------------------------------------------------
// Java – Track‐First (HashMap basiert)
// ---------------------------------------------------
Public class Lösung {\cHFFFF}
Public boolean check Entfernungen(String s, int[] Entfernung) {
Map<Character, Integer> firstPos = new HashMap>();
für (in i = 0; i < s.length(); i++)
n = s.charAt(i);
wenn (firstPos.containsKey(ch)) {
int diff = i - firstPos.get(ch) - 1;
wenn (diff != Distance[ch - 'a']) falsch zurückgegeben wird;
} auch
firstPos.put(ch, i);
}
}
Rückkehr wahr;
}
}

// ---------------------------------------------------
// Java – Check‐Second (auf Platz)
// ---------------------------------------------------
Public class Lösung {\cHFFFF}
Public boolean check Entfernungen(String s, int[] Entfernung) {
für (in i = 0; i < s.length(); i++)
int d = Entfernung [s.charAt(i) - 'a'];
// wenn zweites Auftreten oder aus Grenzen → scheitern
wenn (i + d + 1 >= s.length() || s.charAt(i + d + 1) != s.charAt(i)
Rückgabe falsch;
Entfernung[s.charAt(i) - 'a'] = -1; // Markierung bearbeitet
}
Rückkehr wahr;
}
}
`` `

### 3.2 Python

```python
# ---------------------------------------------------
# Python – Track‐First
# ---------------------------------------------------
Def Check Entfernungen(n): str, Entfernung: list[int]) -> Bool:
= {}
für i, ch in enumerate(s):
wenn ch in first:
falls i - first[ch] - 1 != Distance[ord(ch) - 97]:
Zurück False
andere:
erste[ch] = i
Zurück True

# ---------------------------------------------------
# Python – Check‐Second
# ---------------------------------------------------
Def Check Entfernungen(n): str, Entfernung: list[int]) -> Bool:
für i, ch in enumerate(s):
d = Entfernung [ord(ch) - 97]
wenn i + d + 1 >= len(s) oder s[i + d + 1] != ch:
Zurück False
Entfernung[ord(ch) - 97] = -1 # Marke verarbeitet
Zurück True
`` `

### 3.3 C++

```cpp
#include <bits/stdc++.h>
mit Namespace std;

// ---------------------------------------------------
// C++ – Track‐First
// ---------------------------------------------------
bool check Entfernungen(String s, vector<int>& Distance) {\cHFFFF}
Vektor<int> first(26, -1);
für (int i = 0; i < (int)s.size(); ++i)
int idx = s[i] - 'a';
wenn (erster[idx] != -1)
wenn (i - first[idx] - 1 != Distance[idx]) falsch zurückkehren;
} auch
zuerst[idx] = i;
}
}
Rückkehr wahr;
}

// ---------------------------------------------------
// C++ – Check‐Second
// ---------------------------------------------------
bool check Entfernungen(String s, vector<int>& Distance) {\cHFFFF}
für (int i = 0; i < (int)s.size(); ++i)
int d = Entfernung [s[i] - 'a';
wenn (i + d + 1 >= (int)s.size() || s[i + d + 1] != s[i] falsch zurückkehren;
Entfernung[s[i] - 'a'] = -1; // verarbeitet
}
Rückkehr wahr;
}
`` `

> **Werden Sie den Stil, der sich für Sie am natürlichsten fühlt. **
> *Track‐First* ist ideal für Interviews, die Wert **explicit state tracking** haben.
> *Check‐Second* zeigt **optimierte Einpasslogik** und ein tieferes Verständnis von Array-Indizes.

---

4️⃣ Komplexitätsanalyse

| Operation | Track‐First | Check‐Second |
--------------------------
| Zeit | ` `O(n)` – ein Scan, konstant-time map look‐ups | `O(n)` – ein Scan, Konstant-Zeit-Array-Zugriff |
| Raum | `O(26)` (Karte der ersten Indizes) | `O(1)` – wiederverwendet Eingabefeld |

Beide erfüllen die LeetCode Zwänge bequem (max. `n = 52`).

---

5️⃣ Common Pitfalls (The Ugly)

| Fehler | Warum es scheitert | Fix |
|------------------------------
| **Using `i - firstIndex` statt `i - firstIndex - 1`** | Mis‐counts die Buchstaben *zwischen* Vorkommen. | Subtrahieren 1 um die Endpunkte auszuschließen. |
| **Die Prüfung ist falsch gebunden (`i + d < n` anstelle von `i + d + 1 < n`)** Off-by-one-Fehler beim Vorfahren. | Denken Sie an die `+1` für den Brief selbst. |
| ** Angenommen, alle 26 Buchstaben erscheinen ** | ignorieren das “Unwissen, wenn abwesend” Regel kann zu falschen Positiven / Negativen führen. Verwenden Sie eine Karte oder markieren Sie verarbeitete Einträge; ignorieren Sie Entfernungen, wenn der Buchstabe nie gesehen wird. |
| **Mutating `entfernung` in Check‐ Zweite ohne Kopie** | Nebenwirkungen können in rufenden Code oder Tests übergehen. | Kopieren Sie das Array zuerst (`int[] copy = Distance.clone()`) oder dokumentieren Sie ausdrücklich, dass das Verfahren es mutiert. |

---

6️⃣ Test-getriebene Überprüfung

```text
Prüfung 1
-----
s = "abaccb"
Entfernung = [1,3,0,5,0...]
Ergebnis: true

Prüfung 2
-----
s = "aa"
Entfernung = [1,0,0]
Ergebnis: falsch

Test 3 (Schlitten)
----------
s = "zzxyyzxxzz" // 10 Buchstaben, jeweils zweimal
Entfernung = [0]*26; Entfernung[25] = 8; Entfernung[23] = 2; Entfernung[24] = 1
Ergebnis: true
`` `

Beide Implementierungen auf der gleichen Test-Suite zu laufen garantiert, dass Sie subtile off-by-one Fehler fangen.

---

7️⃣ SEO‐Optimiert Blog Wrap‐ Nach oben

**Titel**
> *Abstände zwischen gleichen Buchstaben prüfen – Java, Python, C++ Lösungen & Interview Tipps*

**Meta-Beschreibung**
> Master LeetCode 2399 mit klaren Java-, Python- und C++-Implementierungen. Erfahre den Track‐First vs. Check‐ Zweite Ansätze, Komplexität und gemeinsame Fallstricke. Erhöhen Sie Ihre Codierung Interview Spiel heute!

**Header Keywords**
- LeetCode 2399
- Distanzen überprüfen Zwischen denselben Buchstaben
- String Algorithmen
- Zwei-Pass-String passend
- Interview Vorbereitung

** Call-to-Action schließen**
> „Wenn Sie für Ihr nächstes Software-Engineering-Interview vorschlagen, üben Sie dieses Problem, bis die Lösung sich zweiter Natur anfühlt. Die Konzepte –Hash-Karten, Zweipunkt-Checks und Off-by-one-Sicherheit – sind über unzählige Codierungs-Herausforderungen wiederverwendbar. „

---

### Final Thought

*Der gute* – Ein unkomplizierter, zeiteffizienter Algorithmus, der eine möglicherweise verwirrende „Distanz“-Regel in einen sauberen, linearen Pass verwandelt.
*Die schlechte* – Die Versuchung zu Hard-Code-Indizes oder ignorieren die “absent Brief”-Regel kann sogar erfahrene Programmierer auslösen.
*The ugly* – Off‐by‐one Fehler, die subtil Lösungen brechen; vermeiden Sie sie durch Doppel-Checking gebunden und mit dem `-1` Trick.

Jetzt, da Sie alle drei Sprachimplementierungen besitzen und die *Warum* hinter jeder Zeile verstehen, sind Sie bereit, LeetCode 2399 zu treffen, beeindrucken Interviewer und landen, dass Jobangebot. 🚀

Glückliche Kodierung!

---

*— Ihr freundlicher Codierer*
<https://www.codemaster.io> | @codeMaster
---

**Happy-Lösungen, und kann Ihr Interview-Code immer off-by-zero korrekt sein! * *