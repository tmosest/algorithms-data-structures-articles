---
Titel: LeetCode 2023. Anzahl der Paare von Strings mit Concatenation Gleiches Ziel -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
# 🧩 LeetCode 2023 – “Anzahl der Paare von Strings mit Concatenation Gleich dem Ziel”

| Sprache | Lösung | Komplexität |
------------------------
| **Java*** | ✅ 1‐pass Hash map | O(n · L) Zeit, O(n) Raum |
| **Python*** | ✅ 1‐pass Hash map | O(n · L) Zeit, O(n) Raum |
| **C++** | ✅ 1‐pass Hash map | O(n · L) Zeit, O(n) Raum |

> *“Wenn Sie einen Tech-Job landen möchten, müssen Sie Probleme meistern, die Ihre Fähigkeit, algorithmisch zu denken und sauberen Code schreiben.”* – **Ihre zukünftigen Interviewer* *

Im Folgenden finden Sie den vollständigen, produktionsfertigen Code für jede Sprache, gefolgt von einem detaillierten Blog-Stil-Auftrag, der das **good, the bad, and the ugly** der Lösung dieses Problems erklärt. Der Artikel ist SEO-optimiert, um Ihnen zu helfen, höher auf Suchmaschinen zu ordnen und von Rekruten bemerkt zu werden.

---

Das Problem (LeetCode 2023)

> **** eine Reihe von Ziffernketten `nums` und eine Ziffernkette `target`, **return** die Anzahl der Indizespaare `(i, j)` (wo `i != j`) so, dass `nums[i] + nums[j] == Ziel.

**Beschränkungen* *

| # Kontraint | Detail |
|--------------------------
| 1 | `2 <= nums.length <= 100` | Small Array size |
| 2 | `1 <= nums[i].length <= 100` | Einzelsaiten können lang sein |
| 3 | `2 <= Target.length <= 100` | Zielstring kann lang sein
| 4 | Alle Strings bestehen aus Ziffern und ** keine führenden Nullen** |

---

🏁 Schnelle Übersicht

ANHANG **Naïve Ansatz** – O(n2) geschachtelte Schlaufen. Arbeitet für die gegebenen Zwänge, ist aber nicht elegant oder skalierbar.
2. **Hash‐Map (Optimal)* – O(n) Zeit, O(n) Raum. Zählen Sie die Ereignisse jedes Strings und schauen Sie dann den komplementären Teil des Ziels auf.
3. ** Warum Hash‐Map?* – Es eliminiert redundante Vergleiche, gibt Konstant-Zeit-Look-ups und hält den Code succinct.

---

Lösungen für Codes

> Alle Lösungen teilen die gleiche Kernidee: Für jeden String `s` in `nums`, wenn `target` mit `s` beginnt, muss der verbleibende Suffix `t` in `nums` existieren (außer wenn `s = t`, müssen wir vermeiden, den gleichen Index zweimal zu zählen).

### 1️⃣ Java

``java
java.util importieren. HashMap;
java.util importieren. Karte;

Public class Lösung {\cHFFFF}
/**
* Zählt die Anzahl der bestellten Paare (i, j), so dass nums[i] + nums[j] == Ziel.
* Zeit: O(n * L)
* Raum: O(n)
*
Int numOfPairs(String[] nums, String Target) {
Map<String, Integer> freq = new HashMap<>();
für (String s : nums) {
freq.put(s, freq.getOrDefault(s), 0) + 1);
}

int count = 0;
für (String s : nums) {
wenn (target.startsWith(s) {
String suffix = Target.substring(s.length());
Int add = freq.get OrDefault(suffix, 0);
wenn (suffix.equals(s) add--; // ausschließen i == j)
Anzahl += add;
}
}
zurückzahlen;
}
}
`` `

### 2️⃣ Python

```python
aus Sammlungen Import Anzahl
aus der Einfuhr Liste

def num_of_pairs(nums: List[str], Ziel: str) -> int:
""
Gibt die Anzahl der bestellten Paare zurück (i, j), wobei nums[i] + nums[j] == Ziel.
Zeit: O(n * L)
Raum: O(n)
""
freq = Zahl(nums)
= 0

für s in nums:
wenn Target.startswith(s):
suffix = Ziel[len(s):]
Anzahl += freq.get(suffix, 0)
wenn suffix == s:
Anzahl 1 # vermeiden i == j)

Anzahl
`` `

### 3️⃣ C++

```cpp
#include <vector>
#include <string>
#include <unordered_map>

int numOfPairs(const std::vector<std::string>& nums, const std::string& target) {\cHFFFF}
std::unordered_map<std::string, int> freq;
für (const auto& s : nums) {
++freq[s];
}

int count = 0;
für (const auto& s : nums) {
wenn (target.rfind(s, 0) == 0) { // Target.startsWith(s)
std::string suffix = Target.substr(s.size());
auto it = freq.find(suffix);
wenn (es != freq.end()) {\cHFFFF}
Zählung += es->se;
wenn (suffix == s) zählen--; // vermeiden i == j)
}
}
}
zurückzahlen;
}
`` `

> Alle drei Snippets kompilieren auf den neuesten JDK 17 / Python 3.10+ / C++17 Compilern und laufen in linearer Zeit.

---

📖 Blog Artikel – „Das Gute, das Schlechte und die Ugly of Pair Concatenation“

> **Titel**: *LeetCode 2023 – Mastering the “Number of Pairs of Strings with Concatenation” Problem (Java, Python, C++)*

### 1. Einleitung

Das "Anzahl der Paare von Strings mit Concatenation Equal to Target"-Problem erscheint trügerisch einfach. Aber es lehrt eine Lektion, die in real‐world codierenden Interviews auftaucht: ** Optimierung von Datenstrukturen und Vermeidung unnötiger Arbeit* kann eine naive O(n2)-Lösung in eine elegante O(n)-Lösung verwandeln.

Unten gehen wir durch das Problem, diskutieren den naiven Ansatz, erklären die optimale Hash‐map-Lösung und reflektieren die *guten, schlechten und hässlichen* Aspekte jedes einzelnen.

> **Warum lesen Sie das? * *
> *Wenn Sie sich auf technische Interviews vorbereiten, wird die Beherrschung dieses Problems nicht nur Ihre LeetCode-Score steigern, sondern Ihnen auch einen Sprechpunkt geben, den Rekrutierer lieben. *

---

### 2. Problem Recap

- **Input**: `nums` – Reihe von Ziffernzeichenfolgen, `target` – Ziffernzeichenfolge.
- **Ausgang**: Anzahl der bestellten Paare `(i, j)` (`i ≠ j`), so dass `nums[i] + nums[j] == Ziel.

*Beispiele*
1. `nums = ["777","7","77","77"], Ziel = "7777" ` → 4 Paare
2. `nums = ["123","4","12","34"], Ziel = "1234" ` → 2 Paare
3. `nums = ["1","1","1"], Ziel = "11" → 6 Paare

Die Schlüsselnuance: **Indizes müssen sich unterscheiden** – der gleiche String-Wert kann mehrfach auftreten, und jedes Ereignis zählt als separater Index.

---

### 3. Der Naïve (Bad) Ansatz

```python
= 0
für i im Bereich(n):
für j im Bereich(n):
wenn i != j und nums[i] + nums[j] == Ziel:
Anzahl 1
`` `

**Pros**
- *Einfach zu schreiben und zu verstehen. *
- Arbeiten unter den kleinen Zwängen des Problems (n ≤ 100).

**Cons**
- **O(n2)* Zeitkomplexität.
- Redundante String-Konzentrationen (`nums[i] + nums[j]`) für jedes Paar.
- Schlechte Skalierbarkeit – würde auf größeren Eingängen auslaufen.

Im Interview ist dies *gut genug für eine schnelle Demo*, aber Rekruten suchen nach *effizienten* Lösungen. Die naive Methode versteckt auch einen subtilen Bug: Wenn `nums[i] == Target`, müssen Sie immer noch sicherstellen, dass der Suffix im Array existiert. Die Hash-map-Lösung behandelt das sauber.

---

### 4. Der optimale (gute) Ansatz – One‐Pass Hash Karte

**Idea**
Für jeden String `s` in `nums`, wenn `target` mit `s` beginnt, muss der verbleibende Suffix `t` irgendwo in `nums` erscheinen. Zählen von Vorkommnissen jeder String können wir `t` in **O(1)* finden.

**Algorithm Steps*

ANHANG **Build Frequency Map*
`freq[s] = Anzahl der Zeiten s erscheint in nums`.

2. **Über jede Strings s**
- Wenn `target` mit `s` beginnt, lassen Sie `t = Target.substring(len(s)) `.
- Fügen Sie `freq[t] zur Antwort hinzu.
- Wenn `t == s`, subtrahieren Sie 1 um die Paarung eines Strings mit sich selbst zu vermeiden (da die Indizes sich unterscheiden müssen).

**Warum es funktioniert* *
- Ja. Wir vergleichen nie jedes Paar.
- Konstant-Zeit-Look-up für den komplementären Teil.
- Linear in `n` (plus die Saitenlänge `L`, die unvermeidbar ist, weil wir `target` inspizieren müssen).

**Komplexe* *
- *Zeit*: `O(n · L)` – `n` Schleifen Iterationen, die jeweils einen Präfix-Check und einen Karten-Lookup machen.
- *Space*: `O(n)` – für die Frequenzkarte.

**Proof of Correctness* *
Jedes bestellte Paar, das die Bedingung erfüllt, wird genau einmal gezählt:

- Angenommen `(i, j)` ist ein gültiges Paar. Lassen Sie `s = nums[i]`.
- In der Schleife für `s`, sehen wir, dass `target` beginnt mit `s`, compute `t = nums[j]`.
- Wir addieren `freq[t]`, die *alle* Indizes `k` so zählt, dass `nums[k] == t`.
- Wenn `k == j`, ist die Addition korrekt; wenn `k == i`, wir subtrahieren 1 wenn `s == t`.

Alle Paare werden erfasst, und keine Fremdpaare werden gezählt.

**Edge Cases Handled*

- Mehrere identische Strings (`["1","1","1"]`).
- Leere Suffix (nur wenn `s` gleich `target`, aber das Problem garantiert `target.length >= 2 `.
- Sehr lange Strings (Konkaten wären teuer, aber Substring Extraktion ist billig).

---

### 5. Implementierung Snippets (One-Pass Hash Karte)

(Siehe den Codeabschnitt oben.)

Alle drei Sprachen teilen die gleiche Struktur:

- Bauen Sie eine `Counter`/`HashMap`/`unordered_map`.
- Verwenden Sie `startsWith`/`target.rfind`/`target.rfind(s, 0)`.
- `suffix = Target[len(s):]` (oder `substr`).
- Frequenz hinzufügen, sich selbst paaren.

---

### 5. Die Ugly – Potenzielle Fallstricke & Gemeinsame Fehler

Warum es passiert | Fix |
|----------------------------------
| **Index-Wert-Kollision** – mit einer von * Wert* markierten Karte, aber vergessen, dass bei verschiedenen Indizes gleiche Werte auftreten können. | Angenommen, jeder Wert ist einzigartig. | Speichern *Frequenz*, nicht eine boolesche Flagge. |
| ** Off‐by‐one in Substring** – Vergessen, `len(s)` anstelle von `s.size()` zu verwenden. | Mismatch zwischen Sprachindex-Konventionen. Testen Sie mit einem Unit-Test, der einzelne Zeichenketten umfasst. |
| **Self‐pairing** – Zählen `(i, i)` wenn `s == t`. | Viele Kandidaten übersehen die `i != j` Regel. | Subtrahieren 1 wenn der Suffix der Präfix-String entspricht. |
| **Large L** – Schnurverkettung in geschachtelten Schlingen kann teuer werden. | Auch wenn `n` klein ist, ist das Prägen von 100-Charakter-Strings 10 000 mal vergeblich. | Vermeiden Sie die Verkettung mit `startsWith`/`substring`. |
| **Case Empfindlichkeit** – Behandlung von `"1" und `"01" anders. | Problem garantiert keine führenden Nullen, aber einige Lösungen mishandle leere Suffixes. | Stellen Sie sicher, `target` Länge ≥ 2 und überprüfen `target.startsWith(s)` zuerst. |

---

### 6. Warum Recruiter die Hash‐Map-Lösung lieben

- **Skalierbarkeit*: Der Code bleibt schnell, auch wenn `n` auf 105 wächst (die Zeitkomplexität ändert sich nicht).
- **Lesbarkeit*: Eine Schleife, ein Karten-Lookup, minimale Verzweigung.
- **Idiomatische Nutzung von Sprachmerkmalen*: Javas `Map.getOrDefault`, Pythons `Counter`, C++s `unordered_map`.
- **Testbarkeit**: Einfach zu testen jede Komponente (Frequenzkarte, Suffixextraktion, Selbstpaareinstellung).

---

### 7. Take-aways für Ihr nächstes Interview

| Tipp | Wie es hilft |
|-----------------------
| **Start mit einer sauberen Frequenzkarte** | Es sagt Ihnen sofort, wie oft ein Substring erscheint. |
| **Avoid Doppelzählung** | Denken Sie daran, dass das Problem nach *ordered* Paaren fragt, so `(i, j)` und `(j, i)` sind deutlich. |
| **Edge‐case first** | Schreibtests für `"1" * 3` & `"11"`, `"777" * 2` & `"7777" `, etc. |
| ** Zeitkomplexitätsangelegenheiten** | Auch wenn die Zwänge klein sind, streben immer lineare oder log‐lineare Lösungen an. |
| **Leverage build‐in helpers** | `String.startsWith()`, `Counter`, `unordered_map` – sie sind unter der Haube optimiert. |

---

### 8. SEO Boost – Keywords & Meta Data

- **Primary Keywords*: LeetCode 2023, Anzahl Paare Verkettung, String Concatenation Problem, optimale Lösung, Hash Map Interview Frage.
- **Secondary Keywords*: Java-Lösung LeetCode, Python-Lösung LeetCode, C++-Lösung LeetCode, Interview Codierungsprobleme, effizienter Algorithmus.

> *Diesen Artikel auf Ihre Portfolio-Site oder LinkedIn Blog hinzufügen und beobachten Sie, dass die Rekrutierer kommen! *

---

### 9. Schluss Gedanken

- Die **naïve-Lösung** ist einfach, scheitert aber am *optimization*-Kriterium.
- Ja. Die **hash‐map-Lösung** ist präzise, skalierbar und zeigt ein tiefes Verständnis der Struktur des Problems.
- **Interviewers** oft Sonde *Warum* Sie eine bestimmte Datenstruktur gewählt haben – bereit sein, den `O(1)` Lookup Vorteil zu erklären.

Üben Sie die drei Implementierungen, führen Sie Ihre eigenen Testbäume und versuchen Sie, das Problem zu erweitern (z.B. nicht-stellige Strings oder größere Arrays zulassen). Das Lernen, das Sie gewinnen, wird für Ihr nächstes Codierungsgespräch unschätzbar sein.

---

### 🎉 Bonus: Quick Test Harness (Python)

```python
def test():
num_of_pairs(["777","7","77","77"], "7777") == ANHANG
num_of_pairs(["123","4","12","34"], "1234") == 2.
num_of_pairs(["1","1","1"], "11") == 6
print("Alle Tests bestanden!")

Test()
`` `

---

Glückliche Kodierung und kann Ihr algorithmischer Geist so scharf sein wie Ihr résumé! 🚀