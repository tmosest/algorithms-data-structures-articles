---
Titel: LeetCode 2644. Finden Sie den maximalen Divisibility Score -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
2644. Finden Sie den maximalen Divisibility Score
**LeetCode 2644 – Easy** | **Java | Python | C++** | **Interview Tipps**

> **Goal** – Für jeden Divisor `d` in `Divisors` zählen, wie viele Zahlen in `nums` durch `d` divisible sind.
> Geben Sie den Divisor mit der Anzahl **maximum** zurück; wenn mehrere Divisors binden, geben Sie die **smallest** ein.

> **Beschränkungen*
> * 1 ≤ `nums.length`, `divisors.length` ≤ 1000
> * 1 ≤ `nums[i]`, `Divisors[i]` ≤ 109

Weil die Grenzen winzig sind, läuft ein gerader Doppel-Loop unter einer Millisekunde. Im Folgenden finden Sie saubere, produktionsfertige Implementierungen in **Java, Python und C++**.

---

oder 1. Java Lösung

``java
// 2644. Finden Sie den maximalen Divisibility Score – Java
Klasse Lösung {
Int maxDivScore(int[] nums, int[] divisors) {\cHFFFF}
// Ergebnis hält den Divisor mit der besten Punktzahl bisher
// maxCount hält seine Partitur
Ergebnis = 0;
int maxCount = -1; // garantiert den ersten Divisor gewinnt Krawatten

für (inte divisor : divisor) {\cHFFFF}
int count = 0;
für (int num : nums) {
(num % Divisor == 0) Graf++;
}
// Aktualisieren, wenn wir eine höhere Punktzahl oder eine gleiche Punktzahl, aber eine kleinere Divisor gefunden haben
wenn (count > maxCount || (count == maxCount && divisor < results) {\cHFFFF}
maxCount = Anzahl;
Ergebnis = Divisor;
}
}
Rückgabeergebnis;
}
}
`` `

**Warum funktioniert es* *

* `O(n · m)` Zeit – zwei geschachtelte Schleifen, jeweils maximal 1000 Iterationen.
`O(1)` extra Platz – nur ein paar ganze Variablen.

---

oder 2. Python Lösung

```python
# 2644. Finden Sie den maximalen Divisibility Score – Python
def maxDivScore(nums: List[int], divisors: List[int]) -> int:
Ergebnis, max_count = 0, -1 # gleiche Idee wie Java
für Divisor in Divisoren:
Anzahl = Summe (1 für num in nums, wenn num % Divisor == 0)
wenn die Anzahl > max_count oder (count == max_count und divisor < result):
max_count = Anzahl
Ergebnis = Divisor
Ergebnis
`` `

*Uses a generator expression for brevity while keep the same `O(n·m)` Laufzeit. *

---

oder 3. C++ Lösung

```cpp
// 2644. Finden Sie den maximalen Divisibility Score – C++
Klasse Lösung {
öffentlich:
int maxDivScore(vector<int>& nums, vector<int>>& divisors) {\cHFFFF}
Ergebnis = 0;
int maxCount = -1;
für (int d : divisors) {\cHFFFF}
int cnt = 0;
für (int num : nums)
wenn 0) ++cnt;
wenn (cnt > maxCount || (cnt == maxCount && d < Ergebnis) {\cHFFFF}
maxCount = cnt;
Ergebnis = d;
}
}
Rückgabeergebnis;
}
};
`` `

*Einfach, lesbar und voll konform mit dem LeetCode Richter. *

---

oder 4. Blog‐Style Walk‐ Durch: Das Gute, das Schlechte und die Ugly

### 4.1 Problem Recap

> **Input** – Zwei Arrays `nums` und `Divisors`.
> **Output*** – Ein Divisor aus `Divisors`, der die meisten Zahlen in `nums` teilt.
> **Tie‐breaker** – Bringen Sie den kleinsten Divisor bei Mehrfachbindung zurück.

### 4.2 Das Gute – Warum der Brute‐Force-Ansatz gewinnt

ANHANG **Simplicity** – Zwei geschachtelte Schleifen, keine zusätzlichen Datenstrukturen.
2. **Correctness by construction* – Jedes Paar von `(Divisor, num)` wird genau einmal untersucht.
3. ** Vorhersehbare Leistung** – `n,m ≤ 1000` Garantien < 1 Million Iterationen, weit unter Zeitlimits.
4. **Easy to test** – Sie können alle Möglichkeiten manuell aufzählen.

### 4.3 The Bad – Wo der Brute‐ Macht die Macht

ANHANG **Skalierbarkeit** – Wenn die Zwänge auf 105 wuchsen, wäre `O(n·m)` unfehlbar.
2. **Cache‐miss heavy** Die innere Schleife ist Speicher für sehr große Arrays gebunden.
3. **Redundante Arbeit* Für jeden Divisor wird der gleiche Modulbetrieb recomputiert.

> *Real‐world Beratung:* Für den produktionsfähigen Code, berücksichtigen Sie die Anzahl der Pre-computing-Divisors oder verwenden Sie eine Hash-Karte, die durch Rest markiert ist. Aber für dieses Problem ist die einfache Lösung optimal.

### 4.4 The Ugly – Edge Cases & Common Pitfalls

Warum es passiert | Fix |
|----------------------------------
| **Wrong tie‐breaker** | Verwenden von `<=` anstelle von `<` bei der Aktualisierung des Ergebnisses. | Verwenden Sie `if (count > maxCount || (count == maxCount && divisor < results) `. |
| ***Initial result value** | Setting `result` to `divisors[0]` und `maxCount` to `0` können einen Divisor mit 0 Score überspringen, wenn alle 0. | Initialise `maxCount = -1` so gewinnt der erste Divisor immer Krawatten. |
| **Overflow** | `num % divisor` passt in `int` für Werte ≤ 109, aber wenn Werte größer wären, brauchen Sie 'long'. |
| **Empty Arrays** | Nicht durch Einschränkungen erlaubt, aber defensive Codierung ist gut. Einen Wächter hinzufügen: if `divisors.isEmpty()` `-1` zurückgeben. |

### 4.5 Komplexitätsanalyse

| Implementierung | Zeit | Raum |
|--------------------------
| Java / Python / C++ | **O(n · m)** | **O(1)* |
| *Erläuterung*: zwei geschachtelte Schleifen, konstante Hilfsgrößen. |

Mit `n, m ≤ 1000` beträgt die schlimmste Laufzeit etwa 1 000 000 Operationen – leicht von jeder modernen CPU zu handhaben.

### 4.6 Interview‐ Fertige Tipps

ANHANG **Erklären Sie die brutale Kraft zuerst* Es zeigt das Verständnis der Problemerklärung.
2. **Mention der Einschränkungen* Zeigen Sie, wo die Lösung effizient ist.
3. **Diskusse mögliche Optimierungen** – Sprechen Sie über Pre-computing Divisor-Sets oder über eine Frequenztabelle, wenn sich Zwänge ändern.
4. **Schreiben Sie sauber, kommentierte Code** – Recruiters lieben beständigen Code.
5. ** Test Randfälle** – Alle Nullen, alle gleichen Zahlen, einzelne Element-Arrays.

### 4.7 Take-away

> Für LeetCode 2644 ist eine Doppel-Loop-Lösung **vollständig ausreichend**.
> Der Schlüssel zur Einstellung des Interviews ist nicht nur der Algorithmus, sondern auch Ihre **Dialogität des Denkens**, **dge‐case sense** und **clean code**.

> Üben Sie ähnliche „Gegen“-Probleme:
> * 1815. Zählen Sie Gegenstände, die eine Regel entsprechen (LeetCode)
> * 1515. Mindestkosten zum Verleih von K Arbeitnehmern (LeetCode)
> Diese verstärken Schleifen, modulare Arithmetik und bindenbrechende Logik.

---

oder 5. SEO‐Optimierte Meta‐Beschreibung (für Ihren Lebenslauf oder Blog)

> „Learn wie man LeetCode löst 2644 – Finden Sie den maximalen Divisibility Score – mit sauberem Java-, Python- und C++-Code. Verstehen Sie Zeit/Raum-Komplexität, bindende Logik und interview-bereite Tipps, um Ihren nächsten Software-Engineering-Job zu landen. „

Fühlen Sie sich frei, die Code-Snippets zu kopieren, den Blog-Post zu veröffentlichen oder die Diskussion in Ihr nächstes Codierungsgespräch einzubinden. Glückliche Kodierung!