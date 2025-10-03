---
Titel: LeetCode 1980. Unique Binary String finden -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
Leetcode 1980 – Einzigartige Binary String finden
**(Java / Python / C++ Lösungen + SEO‐Optimierter Blog Post)**

---

### 1. Code (Alle Sprachen)

oder Java

``java
/**
* Leetcode 1980 – Finde Unique Binary String
* Uhrzeit: O(n)
* Raum: O(1) (Ausgangsstring ignorieren)
*
Klasse Lösung {
public String findDifferentBinaryString(String[] nums) {
int n = nums.length;
StringBuilder sb = neuer StringBuilder(n);
für (in i = 0; i < n; i++) {
// Drehen Sie das Bit an Position i (Cantor's diagonal)
sb.append(nums[i].charAt(i) == '0' ? '1' : '0');
}
sb.toString();
}
}
`` `

Python

```python
Klasse Lösung:
""
Leetcode 1980 – Unique Binary String finden
Zeit: O(n)
Raum: O(1) (ignoring output string)
""
def findDifferentBinaryString(self, nums: List[str]) -> str:
n = len(nums)
# Build the diagonal string by flipping every bit
zurück ''.join('1', wenn nums[i][i] == '0' sonst '0' für i im Bereich(n))
`` `

C++

```cpp
/**
* Leetcode 1980 – Finde Unique Binary String
* Uhrzeit: O(n)
* Raum: O(1) (Ausgangsstring ignorieren)
*
Klasse Lösung {
öffentlich:
String findDifferentBinaryString(vector<string>& nums) {
int n = nums.size();
String res;
res.reserve(n)
für (in i = 0; i < n; ++i) {\cHFFFF}
res.push_back(nums[i][i] == '0' ? '1' : '0');
}
zurück;
}
};
`` `

---

### 2. Blog Artikel – “Das Gute, das Böse und die Ugly von Leetcode 1980”

Titel (SEO-Friendly)
**“Leetcode 1980 – Finden Sie einzigartige Binary String: Java, Python, C++ Solutions + Interview‐Ready Guide”**

Meta Beschreibung
*Master Leetcode 1980 mit sauberem Java, Python und C++-Code. Lernen Sie den optimalen Diagonalisierungstrick, Fallstricke zu vermeiden, und wie Sie diese Interviewfrage zu beantworten. *

---

Einleitung

Wenn Sie sich für eine Software-Engineering-Rolle interviewen, werden Sie auf klassische Probleme „ein fehlendes Element finden“. Leetcode **1980 – Find Unique Binary String** ist ein solches Puzzle, das Ihre Argumentation über Strings, Bitmanipulation und algorithmische Eleganz testet. In diesem Artikel werden wir:

ANHANG **Erklären Sie das Problem* auf Englisch.
2. Gehen Sie durch **Naïve vs. Optimal** Lösungen, was ist “gut”, “schlecht”, und “hässlich. „
3. Bietet **Java, Python und C++** Implementierungen, die in linearer Zeit laufen.
4. Diskutieren Sie Randfälle, Komplexität und interview-freundliche Tipps.

Tauchen wir ein!

---

(Rephrasiert)

Sie erhalten ein Array `nums` von `n` **unique** binäre Strings, jede Länge `n`. Ihre Aufgabe: Erstellen Sie eine binäre Zeichenfolge der Länge `n`, dass ** nicht ** in `nums` erscheinen.

> **Beschränkungen*
> `1 ≤ n ≤ 16`
> - Jeder String besteht nur aus `'0' und `'1'`.
> - Alle Strings in `nums` sind deutlich.

---

Das Gute: Cantor’s Diagonal Trick

Das Problem ist eine Textbuchanwendung von **Cantor’s Diagonalisierung*. Denken Sie an `nums` als `n × n` Matrix von Bits. Durch das Umklappen der Diagonalbits garantieren Sie einen neuen String, der sich von jeder Zeile unterscheidet.

### Warum es funktioniert

- Row `i` hat Bit `nums[i][i]`.
- Das `i`‐th Bit des neuen Strings ist das **gegen*** dieses Diagonalbits.
- Daher kann String `i` nicht mit unserem neuen String an Position `i` übereinstimmen, so dass es nicht mit jeder Zeile identisch sein kann.

**Ergebnis:** Linear-Zeit, Konstant-Raum (ignorieren der Ausgabe) Algorithmus.

---

oder Das Bad: Brute‐ Kraftaufzählung

Eine naive Lösung würde jeden möglichen Binärfaden der Länge `n` erzeugen (es gibt `2^n` Möglichkeiten) und überprüfen, ob es in `nums` ist. Das ist:

- **Time‐Complexity:** `O(2^n)` – undurchführbar auch für `n = 16` (65 536 Kontrollen).
- **Space‐Komplexität:** Möglicherweise groß, wenn Sie alle Kandidaten speichern.

Während dies auf Leetcode durch kleine `n` geht, ist es ein Lehrbuch **O(2^n) Engpass* und sieht schlecht für Interviewer aus.

---

oder Die Ugly: Überkompliziert Hashing

Eine weitere „over-engineering“ Route verwendet ein `HashSet`, um alle Strings zu speichern und dann iterativ die Bits um ein fehlendes zu finden. Es funktioniert, aber:

- Du gibst ein `HashSet` der Größe `n`, was unnötig ist.
- Sie fügen Komplexität hinzu, ohne dass Sie in der Lesbarkeit oder Leistung gewinnen.
- Ja. Der Algorithmus kann für ein solches einfaches Problem "schwer" erscheinen.

### Takeaway

Halten Sie sich an den diagonalen Trick – es ist kurz, klar und mathematisch garantiert.

---

Der Code Walkthrough

Unten sind präzise, idiomatische Lösungen in den drei großen Interviewsprachen.

### 1. Java

``java
Klasse Lösung {
public String findDifferentBinaryString(String[] nums) {
int n = nums.length;
StringBuilder sb = neuer StringBuilder(n);
für (in i = 0; i < n; i++) {
sb.append(nums[i].charAt(i) == '0' ? '1' : '0');
}
sb.toString();
}
}
`` `

*Warum ist das gut: *
- Verwenden Sie `StringBuilder` für O(n) String-Konstruktion.
- Ja. Keine zusätzlichen Datenstrukturen.

### 2. Python

```python
Klasse Lösung:
def findDifferentBinaryString(self, nums: List[str]) -> str:
n = len(nums)
zurück ''.join('1', wenn nums[i][i] == '0' sonst '0' für i im Bereich(n))
`` `

*Pythonic Flair: *
- List‐comprehension verwandelt die Schleife in einen einzigen Ausdruck.

### C++

```cpp
Klasse Lösung {
öffentlich:
String findDifferentBinaryString(vector<string>& nums) {
int n = nums.size();
String res;
res.reserve(n)
für (in i = 0; i < n; ++i) {\cHFFFF}
res.push_back(nums[i][i] == '0' ? '1' : '0');
}
zurück;
}
};
`` `

*C++-Spezifikationen:*
- `reserve(n)` vermeidet Verlagerungen.
- Ternary Operator hält es kompakt.

---

Analyse der Komplexität

| Approach | Zeit | Raum |
|-------------------------
| Cantor Diagonal | **O(n)*** | **O(1)** (Ausgang ausgeschlossen) |
| Brute Force | **O(2n)*** | **O(1)** (Ausgang ausgeschlossen) |
| HashSet Aufzählung | **O(n)** | **O(n)** |

Die optimale Lösung schlägt die Alternativen um den Faktor `2n` und benötigt keine Hilfsspeicherung.

---

Â Edge Cases & Testing

ANHANG **Minimumgröße (`n = 1`)**
- `nums = ["0"] ` → Ausgabe: `"1" `.
- `nums = ["1"] ` → Ausgabe: `"0" `.

2. **Alle Bits Zero**
- `nums = ["00", "01"] → Ausgabe: `"11" `.

3. **Alle Bits One**
- `nums = ["11", "10"] → Ausgabe: `"00" `.

4. **Random Mix**
- Test mit zufälligen binären Strings der Länge `n`.
- Gültig, dass das Ergebnis nicht in `nums` ist.

---

Interview Tipps

| Tipp | Grund |
|-----------------
| **Explain Cantors Diagonalisierung** | Zeigt mathematische Einblicke. |
| **Mention Linearität** | Highlights Effizienz. |
| **Avoid unnötige Datenstrukturen** | Bleibt Lösung schlank. |
| **Zeigen Sie Edge-Case-Handling** | Demonstriert Durchlässigkeit. |
| **Kommentar kurz** | Bewahrt Code lesbar für Rekruten. |

---

Schlussfolgerung

Leetcode 1980 ist deceptiv einfach, sobald Sie das zugrunde liegende Muster erkennen: ein Diagonal-Flip garantiert eine fehlende Zeichenkette. Der diagonale Trick ist Ihre “gute” Lösung – schnell, sauber und mathematisch klingen. Vermeiden Sie brutale Gewalt oder über-engineerierte Hash-Lösungen – sie sind die “schlecht” und “hässliche” Weisen, die Interviewer ablenken.

Indem Sie dieses Problem meistern, erhalten Sie nicht nur die richtige Antwort in einem Bruchteil einer Sekunde, sondern beeindrucken auch Einstellung Manager mit Ihrer algorithmischen Eleganz und Kodierung Disziplin.

Glückliche Codierung und viel Glück Landung diese Software Engineering Rolle!

---

### SEO Highlights

- **Keywords:** Leetcode 1980, Find Unique Binary String, Java-Lösung, Python-Lösung, C++-Lösung, Codierung Interview, Algorithmus Interview, Cantor Diagonalisierung, Job Interview Codierung, Software Engineering Interview.
- **Meta Tags:** `find-unique-binary-string, leetcode-1980, interview-questions, code-interview, algorithm, job-hunting, Java, Python, C++`.

Fühlen Sie sich frei, die Code-Snippets zu kopieren, die Blog-Struktur anzupassen und die Meta-Tags zu Ihrer persönlichen Marke oder Portfolio-Website passen. Viel Glück!