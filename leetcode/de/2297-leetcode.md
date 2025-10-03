---
Titel: LeetCode 2297. Jump Spiel VIII -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
2297. Jump Game VIII – Die Komplettlösung (Java | Python | C++)
### A “Good, Bad, & Ugly” Guide + SEO‐Optimierter Blog Post

---

### TL;DR
| Sprache | Schlüsselidee | Komplexität |
------------------------
| **Java*** | Monotonic‐stack + DP | **O(n)** Zeit, **O(n)** Raum |
| **Python** | Monotonic‐stack + DP | **O(n)** Zeit, **O(n)** Raum |
| **C++** | Monotonic‐stack + DP | **O(n)** Zeit, **O(n)* Raum |

Das Problem fällt auf: Für jeden Index `i` können Sie **once** (oder Nullzeiten) auf das *next* größere oder *next* kleinere Element springen, das die "streng wachsende" oder "streng abnehmende" Lückenregel erfüllt.
Sobald wir das einzige mögliche Ziel für jeden Index kennen, ist der Rest ein klassisches DP: `dp[i] = min(dp[j] + cost[i]) ` über alle erlaubt `j`, die `i` erreichen kann.

Im Folgenden sind saubere, produktionsbereite Implementierungen in **Java, Python und C++** gefolgt von einem SEO-freundlichen Blog-Post, der die Intuition, Fallstricke und Trade‐offs erklärt.

---

oder 1. Das Problem (Re‐Stated)

> **Given**
> - `nums[0...n‐1]` – die „Höhe“ jedes Index
> - `costs[0...n‐1]` – die Kosten für die Landung auf diesem Index
>
> **Sie starten bei Index 0** und können von `i` auf `j` (`i < j`) springen, wenn einer der folgenden hält:
> 1. `nums[i] ≤ nums[j]` **und** Jedes Element zwischen ihnen ist **einschlägig kleiner** als `nums[i]`.
> 2. `nums[i] > nums[j]` **und** Jedes Element zwischen ihnen ist **größer oder gleich** zu `nums[i]`.
> **Goal:** erreicht Index `n‐1` mit minimalen Gesamtkosten (Summe von `costs` jedes gelandeten Index außer Start).

**Beschränkungen*: `1 ≤ n ≤ 105`, `0 ≤ nums[i], Kosten[i] ≤ 105`.

---

oder 2. Intuition & Beobachtung

ANHANG ** Bei den meisten Ausstiegen pro Index**
Wenn Sie von `i` auf zwei verschiedene Indizes `j1` und `j2` springen können, dann können die beiden Bedingungen nicht beide halten. Damit ist gewährleistet, dass die Grafik der möglichen Sprünge eine **-Kollektion von gerichteten Ketten* ist.

2. **Nur das „nächste“ Qualifikationselement zählt**
Für den zunehmenden Fall benötigen Sie nur das *next* Element, das ** ≥ nums[i]** ist; alle früheren würden durch eine kleinere Anzahl blockiert.
Ebenso benötigen Sie für den abnehmenden Fall das *next* Element, das **< nums[i]* ist.

3. **Monotonic Stacks** geben uns genau die "nächsten" Elemente in linearer Zeit.

4. ** Dynamische Programmierung** –
Sobald wir den einzigen zugelassenen Vorgänger für jeden Index kennen, `dp[i] ` ist die Mindestkosten für `i`:
`dp[i] = min(dp[prev] + cost[i]) `prev`, die auf `i` springen kann.
Da jeder Index in jeder Richtung ** ≤ 1* Vorgänger hat, ist der Übergang trivial.

---

oder 3. Ausführung Details

| Sprache | Highlights |
|-------------------------
| **Java*** | Benutzt `ArrayDeque<Integer>` als Stack. `long[] dp` um Überlauf zu vermeiden (`Kosten` bis 105 und `n` bis 105 → 1010). |
| **Python** | Liste als Stack (`append`, `pop`). `float('inf')` für erste dp-Werte. |
| **C++** | `vector<long long>`, `vector<int>\' als Stacks. `numeric_limits<long long>::max()` für INF. |

### 3.1 Java – Monoton Stapel + DP

``java
Import java.util.*;

Public class Lösung {\cHFFFF}
öffentliche lange minCost(int[] nums, int[] kostet) {
int n = nums.length;
lang INF = Long.MAX_VALUE / 4; // Überlauf vermeiden
lang[] dp = neu lang[n];
Arrays.fill(dp, INF);
dp[0] = 0; // Startpunkt kostet nichts

Deque<Integer> incStack = new ArrayDeque<>; // abnehmender Stapel für nächstes >=
Deque<Integer> decStack = new ArrayDeque<>>(); // zunehmender Stapel für den nächsten <

für (in i = 0; i < n; i++) {
// Rechtssache 1: nums[i] >= nums[stack.peek()] → Sprung von Stack.top() nach i
während (!incStack.isEmpty() && nums[i] >= nums[incStack.peek()]) {\cHFFFF}
int j = incStack.pop();
dp[i] = Math.min(dp[i], dp[j] + Kosten[i];
}
// Rechtssache 2: nums[i] < nums[stack.peek()] → Sprung von Stack.top() nach i
während (!decStack.isEmpty() && nums[i] < nums[decStack.peek()] {\cHFFFF}
int j = decStack.pop();
dp[i] = Math.min(dp[i], dp[j] + Kosten[i];
}

incStack.push(i);
decStack.push(i);
}
Rückgabe dp[n - 1];
}
}
`` `

---

### 3.2 Python – Monoton Stack + DP

```python
aus der Einfuhr Liste
Import sys

Klasse Lösung:
def minCost(self, nums: List[int], Kosten: List[int]) -> int:
n = len(nums)
INF = 10 ** 18
dp = [INF] * n
dp[0] = 0

Inc_stack = [] # Stack for next >= (monoton abnehmend)
dec_stack = [] # Stapel für nächstes < (monotones Ansteigen)

für i im Bereich(n):
während inc_stack und nums[i] >= nums[inc_stack[-1]]:
j = inc_stack.pop()
dp[i] = min(dp[i], dp[j] + Kosten[i])

während dec_stack und nums[i] < nums[dec_stack[-1]:
j = dec_stack.pop()
dp[i] = min(dp[i], dp[j] + Kosten[i])

inc_stack.append(i)
dec_stack.append(i)

zurück dp[-1]
`` `

---

### 3.3 C++ – Monotonic Stack + DP

```cpp
#include <bits/stdc++.h>
mit Namespace std;

Klasse Lösung {
öffentlich:
lange minCost(vector<int>& nums, vector<int>>&kosten) {\cHFFFF}
int n = nums.size();
const lang INF = LLONG_MAX / 4;
Vektor<long long> dp(n, INF)
dp[0] = 0;

Vektor<int> incStack; // abnehmender Stapel für nächstes >=
vektor<int> decStack; // Stapelbildung für nächsten <

für (in i = 0; i < n; ++i) {\cHFFFF}
während (!incStack.empty() && nums[i] >= nums[incStack.back()]) {\cHFFFF}
int j = incStack.back();
IncStack.pop_back();
dp[i] = min(dp[i], dp[j] + Kosten[i];
}
während (!decStack.empty() && nums[i] < nums[decStack.back()] {\cHFFFF}
int j = decStack.back();
decStack.pop_back();
dp[i] = min(dp[i], dp[j] + Kosten[i];
}
incStack.push_back(i);
decStack.push_back(i);
}
zurückgeben dp.back();
}
};
`` `

---

oder 4. Blog Post – “Das Gute, das Schlechte und die Ugly von Jump Game VIII”

> **Titel:** *Jump Spiel VIII: Von Monoton Stacks zu O(n) DP – A Complete Guide*
> **Keywords:* LeetCode 2297, Jump Game VIII, Dynamische Programmierung, Monotonischer Stack, Java, Python, C++, Interview Prep, Algorithm Analysis

---

### Einführung

LeetCodes *Jump Game VIII* (Problem 2297) sitzt auf der „mittleren“ Schwierigkeitsstufe, aber seine Drehung auf der klassischen Jump-Game-Erzählung kann sogar saisonale Coder auslösen. Der Schlüssel ist zu erkennen, dass jeder Index ** bei den meisten ** ausgehenden Sprung in jede Richtung hat, dank der strengen “Gap” Regeln. Diese Beobachtung verwandelt ein scheinbar grafisch-schweres Problem in eine ordentliche DP, die in **O(n)* Zeit mit **monotonen Stapeln** gelöst werden kann.

Lassen Sie uns nicht erkennen, was dieses Problem **good** macht, welche Fallstricke (die **bad**) darunter laudern und wo die Lösung **ugly*** werden kann, wenn wir nicht vorsichtig sind.

---

oder Das Gute

ANHANG **Linear Zeit und Raum*
Der monotone Stack-Ansatz garantiert `O(n)` Laufzeit und `O(n)` Hilfsraum. Dies ist für die gegebenen Zwänge kritisch (`n ≤ 105`).

2. **Single Pass, Zwei Stapel**
Durch die Verarbeitung von Indizes links-rechts und die Aufrechterhaltung von zwei Stapeln (eine abnehmende, eine Erhöhung), können wir gleichzeitig die *nächste größer* und *nächste kleinere* Übergänge ohne Rückverfolgung behandeln.

3. **Clean DP Transition* *
Da jeder Index in jeder Richtung höchstens einen Vorgänger hat, reduziert sich die DP-Rekursion auf einen einzigen `min`-Betrieb. Kein Bedarf an geschachtelten Schleifen oder komplexen Zustandsverfolgung.

4. **Language-agnostik**
Die gleiche Logik übersetzt nahtlos in Java, Python und C++, so dass es eine ausgezeichnete Interview “portable” Lösung.

---

oder Das Böse

ANHANG ** Überflussrisiko**
`costs[i]` kann bis zu `105` sein und Sie können bis zu `105` Sprünge ketten. Die Verwendung von `int` für `dp` wird überlaufen. Alle Implementierungen verwenden `long`/`long long` und einen sicheren INF-Wert.

2. **Stack Growth Missverständnis* *
Es ist einfach zu verwechseln “next größer oder gleich” mit “next streng größer.” Die erste Bedingung des Problems erlaubt Gleichheit (`nums[i] ≤ nums[j]`). Die Stacklogik muss beim Popping die richtige Ungleichheit bewahren.

3. **Edge Cases*
- Wenn `n = 1`, die Antwort ist trivial `0`.
- Wenn das erste Element keinen anderen Index erreichen kann (z.B. ein streng abnehmendes Array), bleibt das DP bei INF für nicht erreichbare Indizes – der Code muss dies anmutig handhaben.

4. **Memory Footprint* *
Mit einem `Deque<Integer>` oder `vector<int>` für die Stapel können zusätzliche Speicherkosten, wenn Sie alle Indizes drücken. Allerdings wachsen die Stacks nie über `n` hinaus, so bleibt der Gesamtspeicher `O(n)`.

---

oder Die Ugly

ANHANG **Hard to Read without Comments*
Die zweistapelige Logik sieht auf den ersten Blick kryptisch aus. Inline-Kommentare oder ein Diagramm im Produktionscode hinzufügen, verbessert die Aufrechterhaltungsfähigkeit.

2. **Stack Auftragsfehler* *
Wenn Sie Indizes auf den falschen Stack drücken oder vergessen, `dp[i]` vor dem Schieben zu aktualisieren, wird die Lösung leise falsch, was schwerer zu debug ist, weil alle Übergänge in einem einzigen Pass auftreten.

3. **Non‐Monotonic Durchführung* *
Ein naiver Ansatz, der das Array für das „nächste“ Qualifying-Element für jeden Index (O(n2)) scannt, ist technisch korrekt, wird aber zeitout. Vermeiden Sie solche „hässlichen“ quadratischen Lösungen, es sei denn, Sie befinden sich in einem sehr eingeschränkten Interview.

4. **Copy‐Paste Boilerplate* *
In Interviews, Menschen oft copy‐paste Kesselplatte ohne Anpassung INF oder Stack-Größen, was zu subtilen Bugs.

---

### Step‐by‐Step Beispiel

> **Array*: `nums = [2, 1, 4, 3] `
> **Kosten**: Kosten = [0, 5, 2, 1]

| Index | `nums[i]` Von 'incStack'? | Popped from `decStack`? | `dp[i]` nach Übergängen |
---------------------------------------------------------------------------------------------
| 0 | 2 | – | – | 0 |
| 1 | 1 | – | pop (0) → `dp[1] = 0 + 5 = 5` | 5 |
| 2 | 4 | pop (1) → `dp[2] = 5 + 2 = 7` | – | 7 |
| 3 | 3 | – | pop (2) → `dp[3] = 7 + 1 = 8` | 8 |

Ergebnis: `dp[3] = 8` – die Mindestkosten, um den letzten Index zu erreichen.

Ein schnelles Diagramm kann den Lesern helfen, die beiden gerichteten Ketten zu visualisieren.

---

### Letzte Gedanken

Jump Game VIII zeigt die Schönheit der algorithmischen Reduktionen: ein Problem, das sich wie ein Graph Traversal fühlt, ist mit der richtigen Beobachtung ein klassisches DP gelöst mit zwei monotonen Stacks. Halten Sie ein Auge auf ganzzahlige Überlauf, Ungleichheiten und Rand-Fälle, um das *bad* zu vermeiden, und fügen Sie klare Kommentare zu tame die *ugly*.

Glückliche Codierung, und können Ihre Sprünge immer minimal sein!

---

### Referenzen & Weiteres Lesen

- LeetCode 2297 – [Problem Statement](https://leetcode.com/Probleme/jump-game-iv/)
- *Einführung zu Monotonic Stacks* – [GeeksforGeeks](https://www.geeksforgeeks.org/stack-data-structure/)
- * Dynamische Programmierung 101* – *Cracking the Coding Interview*, 7. Auflage.

---

**Autor:** [Ihr Name] – Interview Coach, Algorithm Enthusiast, Open Source Contributor.
**Kontakt:** `youremail@example.com `

---

oder 5. Letzte Checkliste

- [ ] Verwenden Sie `long`/`long long` für DP, um Überlauf zu vermeiden.
- [ ] Stellen Sie sicher, dass der Stack-Pop-Zustand `≤` vs `< ` respektiert.
- [ ] Griff `n == 1` sofort.
- [ ] Fügen Sie Kommentare oder Diagramme zur Klarheit im realen Interview oder Produktionscode hinzu.
- [ ] Testen Sie gegen zufällige Fälle, insbesondere Rand-Arrays (senkt ansteigend/abnehmend).

Mit diesem, Sie sind voll ausgestattet, um *Jump Game VIII* in jeder Interview-Einstellung und jede Programmiersprache, die Sie bevorzugen. Glückliche Kodierung!

---