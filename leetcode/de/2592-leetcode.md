---
Titel: LeetCode 2592. Maximize Größe eines Arrays -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
2592. ** Maximale Größe eines Arrays**
### A Complete, Interview‐Ready Guide
*(Java | Python | C++)*

---

### TL;DR
- **Goal:* Um die Anzahl der Indizes zu maximieren, bei denen der neue Wert * begrenzt größer * als der ursprüngliche Wert ist.
- **Greedy / Two‐Pointer Trick:** Sortieren Sie `nums` aufsteigend, dann verwenden Sie zwei Indizes (`i` – “candidate” Element, `j` – “current” Position), um das kleinste Element auszuwählen, das `nums[j] schlägt.
- ** Zeitkomplexität:** `O(n log n)` (für die Sortierung).
- **Space-Komplexität:** `O(1)` Hilfsmittel (wenn wir an Ort und Stelle sortieren) oder `O(n)` wenn wir eine Kopie benutzen.

---

oder 1. Problem Recap

> ** Bestimmung der Größe* *
> Für eine Permutation `perm` des ursprünglichen Arrays `nums` ist die *Greatness* die Anzahl der Indizes `i`, wo `perm[i] > nums[i]`.

> **Task**
> Rückgabe der maximal möglichen Größe nach jeder Permutation von `nums`.

---

oder 2. Intuition & Strategie

ANHANG **Sortieren Sie das Array**
Sortieren gibt uns die kleinsten verfügbaren Zahlen an der Front, die perfekt für einen gierigen Ansatz ist: wir wollen die kleinste Zahl, die noch ein bestimmtes Element schlagen kann.

2. ** Zwei Zeiger**
- `i` – scannt durch das sortierte Array (die „Kandidaten“-Werte).
- `j` – scannt das ursprüngliche Array (die "Ziel"-Indizes).
Wir versuchen, den kleinsten Kandidaten zu koppeln, der *größer* ist als das aktuelle Ziel.

3. **Warum gierige Werke* *
- Wenn wir einen Kandidat `c` haben, der `nums[j] ` schlägt, kann die Antwort hier nicht verschlechtern später, weil jeder größere Kandidat auch `nums[j] ` schlagen könnte.
- Mit dem kleinsten möglichen Kandidat gibt es größere Zahlen für später zur Verfügung, maximieren zukünftige Möglichkeiten.

---

oder 3. Algorithm (Pseudocode)

`` `
sort(nums) // aufsteigen
i = 0 // Kandidatenindex
= 0

für j in 0 .. nums. Länge-1: // j ist der Zielindex
während i < nums.length und nums[i] <= nums[j]:
= 1 // alle Zahlen überspringen, die nicht geschlagen werden können [j]
wenn i == nums.length:
Pause // keine Kandidaten mehr übrig
Anzahl += 1 // nums[i] schlägt nums[j]
i += 1 // Wechsel zum nächsten Kandidaten

Anzahl
`` `

---

oder 4. Komplexitätsanalyse

| Betrieb | Kosten |
|------------------
| Sortierung | `O(n log n)` |
| Zweipunkt Scan | `O(n)` |
| Gesamtzeit | **`O(n log n)** |
| Extrafläche | **`O(1)`* (in‐Ort-Sort) oder `O(n)``` wenn eine Kopie benötigt wird |

Die Zwänge (`n ≤ 105`) werden von diesem Ansatz bequem behandelt.

---

oder 5. Code Implementierungen

Unten sind saubere, produktionsfertige Lösungen in **Java*, **Python** und **C++**.

---

### 5.1 Java

``java
java.util importieren. Strahlen;

Public class Lösung {\cHFFFF}
Int maximizeGreatness(int[] nums) {
// Sortieren Sie das Array, um die Zweipunkt-Grady-Strategie zu aktivieren
Arrays.sort(nums);
int n = nums.length;
int i = 0; // Kandidat Pointer
int count = 0;

// Traverse Original Indizes
für (int j = 0; j < n; j++) {\cHFFFF}
// Advance i bis wir eine Zahl finden, die Nums schlägt[j]
(i < n && nums[i] <= nums[j]) {\cHFFFF}
i++;
}
wenn (i == n) Pause; // keine Kandidaten mehr
Anzahl++; // nums[i] > nums[j]
i++; // diesen Kandidaten benutzen
}
zurückzahlen;
}

// Schneller Prüfgurt
öffentliche statische Leerstelle (String[] args) {
Lösungssol = neue Lösung();
System.out.println(sol.maximizeGreatness(new int[]{1,3,5,2,1,3,1})); // 4
System.out.println(sol.maximizeGreatness(new int[]{1,2,3,4})); // 3
}
}
`` `

---

### 5.2 Python

```python
Klasse Lösung:
def maximieren Größe(selbst, nums: list[int]) -> int:
nums.sort() # in‐place sort
n = len(nums)
i = 0 # Kandidatenindex
= 0

für j im Bereich(n):
wenn i < n und nums[i] <= nums[j]:
= 1
wenn i == n: # keine Kandidaten mehr
Bruch
Anzahl 1
= 1

Anzahl

# Quick test
wenn __name__== "__main__":
sol = Lösung()
print(sol.maximizeGreatness([1, 3, 5, 2, 1, 3, 1])) # 4
print(sol.maximizeGreatness([1, 2, 3, 4]) # 3
`` `

---

5.3 C++

```cpp
#include <bits/stdc++.h>
mit Namespace std;

Klasse Lösung {
öffentlich:
int maximieren Größe(vector<int>& nums) {
sort(nums.begin(), nums.end()); // aufsteigend
int n = nums.size();
int i = 0; // Kandidat Pointer
int count = 0;

für (int j = 0; j < n; ++j) {
(i < n && nums[i] <= nums[j]) ++i;
wenn (i == n) Pause; // keine Kandidaten mehr
++count; // nums[i] > nums[j]
++i;
}
zurückzahlen;
}
};

// Schnelltest
int main() {\cHFFFF}
Lösungssol;
cout < < sol.maximizeGreatness({1,3,5,2,1,3,1}) << endl; // 4
cout < < sol.maximizeGreatness({1,2,3,4}) << endl; // 3
Rückkehr 0;
}
`` `

---

oder 6. Blog Artikel – „Das Gute, das Schlechte und die Ugly von LeetCodes Maximize Greatness Problem“

### 6.1 Warum dieses Problem ein großes Interview Show-Topper ist

- **Inbegriffstiefe:** Es testet *Grady* Argumentation, * Zwei-Punkte* Tricks, und ein Verständnis, das Sortieren kann versteckte Struktur entsperren.
- **Sprachdiagnose:** Ihre Lösung funktioniert in Java, Python, C++, Geh, Rust – die gleiche Idee, nur verschiedene Syntax.
- **Skalierbar:** Mit `n = 105` würde ein naïve `O(n2)`-Ansatz zeitout, so dass Interviewer schätzen eine `O(n log n)`-Lösung.

### 6.2 The Good

| Aspect | Warum es gut ist |
|--------------------------
| **Simplicity** | Nach der Sortierung reduziert sich die Logik auf einen einzigen linearen Pass. |
| **Deterministisch** | Kein Zufall oder heuristisch. |
| **Deterministische Zeit** | `O(n log n)` ist auch für große Eingänge akzeptabel. |
| ** Breite Anwendbarkeit** | Die gierige Technik ist wiederverwendbar (z.B. "Permuting Two Arrays" Problem). |

### 6.3 The Bad

| Ausgabe | Mitigation |
|----------------------
| **Sortierungskosten** | Für extrem große Arrays (`n > 106`) benötigen Sie möglicherweise eine Zähl- oder Bucketsort, aber hier nicht benötigt. |
| **In‐place Mutation** | Einige Interviewer bitten, das ursprüngliche Array zu erhalten; Sie können eine Kopie vor der Sortierung machen. |
| **Edge Cases** | Alle gleichen Elemente → beantworten `0`. Leere Array (nicht in Zwängen) → behandeln anmutig. |

### 6.4 The Ugly

- ** Missverständnisse „größer als“**: Einige Kandidaten verwenden versehentlich “≥” anstelle von “>”, wodurch off-by-one Fehler.
- **Pointer Overrun**: Vergessen, `i < n` innerhalb des inneren `While` zu überprüfen, kann zu einem `ArrayIndexOutOfBoundsException` in Java oder Segmentierungsfehler in C++ führen.
- **Sorting Nebenwirkungen*: Wenn das Interview den ursprünglichen Auftrag für einen späteren Gebrauch erfordert, denken Sie daran, das Array zuerst zu kopieren.

### 6.5 SEO‐ Mit freundlichen Grüßen

Wenn Sie nach *“LeetCode 2592 Lösung”* oder *”maximieren Sie die Größe eines Array-Interviews”* suchen, ist dieser Leitfaden Ihr One-Stop-Shop:

- **Titel*** – *LeetCode 2592 – Maximieren Sie die Größe eines Arrays – Java, Python, C++ Lösungen*
- **Meta Beschreibung** – „Lesen Sie, wie man LeetCode 2592 mit effizientem Java-, Python- und C++-Code löst. Verstehen Sie den gierigen Zwei-Punkter-Ansatz, Randfälle und Interview-Tipps. „
- **Keywords** – LeetCode, Maximize Greatness, Array Permutation, zwei Pointer, gieriger Algorithmus, Codierung Interview, algorithmische Herausforderung, Java-Lösung, Python-Lösung, C++-Lösung, Job Interview Prep.

---

oder 7. Schlussworte – Wie man das Interview vernichtet

ANHANG **Erklären Sie die gierige Idee** – „Sort the array, so dass wir immer die kleinste Zahl auswählen können, die das aktuelle Ziel schlägt. „
2. **Mention Time/space** – „Wir sortieren `O(n log n)` und führen dann einen linearen Scan durch. „
3. **Cover Randfälle** – „Alle Elemente gleich → 0; Arraygröße 1 → 0.“
4. **Zeigen Sie den Code** – Geben Sie die saubere, kommentierte Lösung in der Sprache Ihrer Wahl.
5. ** Hohe Wiederverwendbarkeit** “Das gleiche Muster löst ‘Permuting Two Arrays’ und viele “Beat‐the‐target” Probleme. „

Mit diesem Ansatz werden Sie ein scheinbar komplexes LeetCode-Problem in ein Schaufenster von sauberem Algorithmus-Design und solide Codierung Fähigkeiten verwandeln – genau das, was Rekrutierer wollen. Viel Glück!