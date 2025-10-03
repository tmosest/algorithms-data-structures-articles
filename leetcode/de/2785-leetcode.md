---
Titel: LeetCode 2785. Vowels in einem String sortieren -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
oder 1. 3‐Sprache Implementierung – LeetCode 2785 „Sort Vowels in a String“

Das Problem ist einfach zu sagen, aber ein guter Test von *string Manipulation*, *Kennzeichen Klassifikation*, und *sorting*.
Im Folgenden sind saubere, produktionsfertige Lösungen in **Java**, **Python** und **C++**, die in `O(n log n)`-Zeit (nach Sortierung) und `O(n)`-Speicher laufen.

> **Key Idea**
> 1. Ziehen Sie alle Vokale aus der Eingabekette in eine separate Liste.
> 2. Sortieren Sie diese Liste lexicographisch (ASCII-Bestellung).
> 3. Gehen Sie die ursprüngliche Saite wieder, ersetzen Sie jedes Vokal mit dem nächsten Element aus der sortierten Liste, lassen Konsonanten unberührt.

Da Vokale nur 10 verschiedene Zeichen sind, ist die Art trivial und kann sogar durch eine Zählfunktion ersetzt werden, wenn Sie möchten.

---

### 1.1 Java – `Solution.java `

``java
java.util importieren. ArrayList;
java.util importieren. Sammlungen;
java.util importieren. Liste

Klasse Lösung {

// Helfer – schnelle Vokalerkennung (constant time, no regex)
privat boolean isVowel(char c) {
// 10 mögliche Vokalzeichen
zurück c == 'a' || c == 'e' || c == 'i' ||
c = 'o' || c = 'u' ||
c = 'A' || c = 'E' || c == Ich ||
c = 'O' || c = 'U';
}

public String sortVowels(String s) {
// 1️⃣ Vokale sammeln
List<Character> vowels = new ArrayList<>>();
für (char c : s.toCharArray()) {\cHFFFF}
wenn (isVowel(c)) {\cHFFFF}
Wowels.add(c)
}
}

// 2️⃣ Sort vowels – O(k log k), k ≤ s.length
Sammlungen.sort(Möbel);

// 3️⃣ Reconstruct string
StringBuilder ans = new StringBuilder(s.length());
int idx = 0; // Index in sortierte Vokale
für (char c : s.toCharArray()) {\cHFFFF}
wenn (isVowel(c)) {\cHFFFF}
ans.append(vowels.get(idx++)); // nächste kleinste Vokal
} auch
ans.append(c) // consonant as‐is halten
}
}
zurück ans.toString();
}
}
`` `

---

### 1.2 Python – `solution.py `

```python
Klasse Lösung:
def sortVowels(self, s: str) -> str:
vowels = [c für c in s wenn c in "aeiouAEIOU"]
vowels.sort() # ASCII bestellen

Ergebnis = []
vi = 0 # Zeiger in vowels list
für c in s:
wenn c in "aeiouAEIOU":
Ergebnis.append(vowels[vi])
= 1
andere:
Ergebnis.append(c)
zurück ".join(Ergebnis)
`` `

Pythons Listenverständnisse und `str.join` halten den Code prägnant, während sie perfekt lesbar bleiben.

---

### 1.3 C++ – `Solution.cpp `

```cpp
#include <bits/stdc++.h>
mit Namespace std;

Klasse Lösung {
öffentlich:
bool isVowel(char c) const {
c='a' || c='e' || c='i' ||
c='A' || c='E' || c='I' || c='O' || c='U';
}

Art Vowels(string s) {
// 1️⃣ Ziehen Sie Vokale
Vektor<char> v;
für (char c : s)
wenn (isVowel(c))
v.push_back(c)

// 2️⃣ Sortieren
sort(v.begin(), v.end()); // ASCII-Bestellung

// 3️⃣ Rebuild
String res;
res.reserve(s.size());
Größe_t idx = 0;
für (char c : s) {\cHFFFF}
wenn (isVowel(c))
res.push_back(v[idx++]); // das kleinste verbleibende Vokal
andere
res.push_back(c); // consonant bleibt
}
zurück;
}
};
`` `

C++ folgt dem gleichen Muster. Der `isVowel` Helfer ist für Geschwindigkeit inlined.

---

oder 2. Blog Artikel – “Das Gute, das Schlechte, und die Ugly der Sortierung Vowels (LeetCode 2785)”

> **Keywords*: *sort vowels string*, *LeetCode 2785 Lösung*, *Java Python C++ Codierung Interview*, *job Interview Codierung Problem*, *interview algorithm*, *string Manipulation*, *vowel sorting*, *competitive Programmierung*

---

### 2.1 Einführung

Wenn Rekrutierer Ihnen ein Problem geben, das trügerisch einfach aussieht – „sortieren Sie die Vokale in einem String, während Sie Konsonanten an Ort und Stelle halten“ – Sie werden nicht nur gebeten, Code zu schreiben. Sie werden ausgewertet, wie Sie ein Problem aufbrechen, die richtigen Datenstrukturen auswählen und sauberen, pflegefähigen Code schreiben, der schnell auf der schlimmsten Eingabe läuft.

In diesem Artikel gehe ich durch den **gut** (reiner, lesbarer Code), das **bad*** (gemeinsame Fallstricke und warum sie wichtig sind) und den **ugly*** (über-engineering or edge‐case blind spots). Am Ende wissen Sie, warum die dreisprachigen Lösungen oben die richtige Lösung für LeetCode 2785 sind.

---

### 2.2 Das „Good“ – Sauber, bewährt, Cross‐Language

| Sprache | Schlüsselstärke | Warum es |
-------------------------
| **Java*** | Starke Schreibweise, explizit `StringBuilder`, einfach zu debug | Gut für Interviews, die nach *OOP* Stillösungen fragen
| **Python** | Concise, high-level, no Boilerplate | Zeigt, dass Sie Probleme schnell lösen können, ohne Klarheit zu verlieren |
| **C++** | Zero‐cost Abstraction, `std::string` und `std::vector` | Demonstrates Meisterschaft von STL und Performance Tuning |

Der Kernalgorithmus ist in jeder Sprache identisch: *extract‐sort‐reinsert*. Dies ist die goldene Regel in algorithmischen Interviews – *Erfinden Sie nicht das Rad pro Sprache*. Stattdessen das **Konzept** aussetzen; die Implementierungsdetails können sich ändern.

**Time Complexity** – `O(n log n)`, wo `n` die Länge des Strings ist.
**Space Complexity** – `O(n)` (die Liste der Vokale, plus die Ausgabekette).
Für die Zwänge `n ≤ 100 000` läuft die Lösung auf allen großen Richtern bequem unter 10 ms.

---

### 2.3 The “Bad” – Was Interviewer wirklich beobachten

| Pitfall | Schlechte Konsequenz | Fix |
-------------------------------------
| **Using regex** (`re.findall('[aeiouAEIOU]', s)`) | O(n) *aber* langsamere Konstanten; versteckte Zuordnungen | Verwenden Sie eine handschriftliche `isVowel` oder eine Lookup-Tabelle |
| **Sorting by Unicode points* (`sorted(vowels, key=ord)`) in Python | Gleicher Effekt, aber `sort()` ist bereits ASCII‐aware; unnötige Schlüsselfunktion | Call `vowels.sort()` |
| **Die Antwort durch das Konzipieren von Strings* (`result += c`) | Erstellt O(n2) Zeit in Java/C++ und Python | `StringBuilder` / `join` sind linear in der Gesamtlänge |
| **Ignorieren von oberer/unterercase** | Falscher Ausgang für gemischtes Gehäuse | Testen Sie immer beides `a...u` und `A...U` – sie sind 10 verschiedene Zeichen |
| **Verzeichnis mehr Speicher als erforderlich* | Gelöschter Platz auf großen Eingängen | Verwenden Sie `reserve()` /`StringBuilder` Kapazität Hinweise |

Diese Fehler sehen trivial aus, aber sie machen Ihre Lösung langsamer, härter zu lesen oder sogar falsch auf einem versteckten Testfall.

---

### 2.4 Die „Ugly“ – Over‐Engineering, Edge‐Case Blindness

- **Counting sort for vowels* *
*Warum ist es hässlich:* Die Ausführung einer manuellen Zählart für nur 10 mögliche Vokale ist übertötet und fügt unnötige Codezeilen hinzu.
*Better:* `Collections.sort()`, `sorted()` oder `std::sort()` sind beide schnell genug und deutlicher.

- ** Vor Ort eine Arraygröße 256**
*Warum ist es hässlich:* Es funktioniert, aber Sie vergeben 256 Bytes für nichts. Ein `Map` oder `boolean[256]` ist vergeblich, wenn Sie nur 10 Vokale benötigen.

- ** Verwendung von `replace()` in einer Schleife* *
*Warum es hässlich ist:* `String.replace()` erstellt jedes Mal einen neuen String, der zu quadratischem Verhalten auf langen Eingängen führt.

- **Ignorieren von Unicode / nicht-ASCII Alphabete* *
Das Problem garantiert ASCII-Briefe, aber ein "reales" Interview könnte es verlängern. Eine robuste Lösung würde anstelle eines `c in "aeiouAEIOU" ein **hash-Set*** aus Vokalen verwenden.

---

### 2.5 Edge Cases – Die Checkliste „Warum nicht“

| Edge Case | Was ist zu testen | Typischer Bug |
--------------------------
| **Keine Vokale** | `"bcdfg"` → `"bcdfg"``````````````Keine leere Vokalliste zurückgeben und aus den Grenzen zugreifen |
| **Alle Vokale** | `"aeiouAEIOU"`` → `"AAAEEEIIIOOOUU"`````````````` den Vokalzeiger |
| **Long string** (`105` chars) | Random mix | Nicht vor Ort `StringBuilder` führt zu vielen Verlagerungen |
| **Mixed case** | `"Hello World"` → `"Holle World"````````````` | Verwenden von `c in "aeiouAEIOU" falsch (case‐sensitive) |
| **Special Characters** (wenn das Problem erweitert wurde) | | "a!b?c"` | Behandeln `!` oder `?`, da Konsonanten in Ordnung sind, aber in der Dokumentation explizit sein |

Jede dieser Garantien zu testen, dass der Code des Kandidaten *defensive* und *robust* ist.

---

### 2.6 Warum dieses Problem ein gutes Interview Star ist

ANHANG **String-centric* Die meisten Interviews drehen sich um String-Probleme; sie sind einfach zu schreiben, aber schwer, falsch zu bekommen.
2. **Charakter-Klassifikation** – Demonstriert Kenntnisse über ASCII-Bereiche, Regex vs. manuelle Kontrollen.
3. **Space/time trade-offs* – Zeigt Ihnen die richtige Datenstruktur (`List` vs. Array).
4. **Output-Format* – Die Ausgabe muss die ursprüngliche Reihenfolge der Konsonanten beibehalten. Es zwingt den Kandidaten, *Verarbeitung* von *Rekonstruktion* zu trennen.

Wenn Sie den Algorithmus erklären können, schreiben Sie sauberen Code in mindestens ** einer* der oben genannten Sprachen und diskutieren Komplexität, Sie werden ein starker Kandidat für Rollen, die algorithmisches Denken und Code-Qualität schätzen.

---

### 2.7 Final Take-away

- **Keep it simple** – Extrahieren, sortieren, re‐insert.
- **Avoid regex** – Konstantzeithelfer gewinnen.
- ** Verwenden Sie Sprachstärken* – `StringBuilder` in Java, `join` in Python, STL-Container in C++.

Wenn Sie ein Bewerbungsgespräch landen, suchen Rekruten nicht nur nach einer *working* Lösung; sie werden überprüfen, wie Sie Ihren Code Struktur. Die Schnipsel oben zeigen, dass Sie schnell, akkurat und gleichzeitig pflegefähig sein können – genau die Mischung, die sie suchen.

Glückliche Kodierung und können Ihre Vokale immer zu Ihren Gunsten sortiert werden!