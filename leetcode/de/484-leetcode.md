---
Titel: LeetCode 484. - Ja.
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
Leetcode 484 – Permutation finden
### “Das Gute, das Schlechte und die Ugly” eines klassischen Interview-Problems
*(Java | Python | C++) – O(n) Zeit, O(1) Hilfsraum)*

---

### TL;DR
* **Problem** – Bauen Sie die lexikographisch kleinste Permutation von `[1 ... n], die ein Muster von “I” (Erhöhung) und “D” (Erhöhung) erfüllt.
**Solution*** – Scannen Sie einmal den String und wann immer ein Ablauf von aufeinanderfolgenden „D“ gefunden wird, kehren Sie diesen Abschnitt der natürlichen Ordnung `[1, 2, ...] um.
* **Warum ist es wichtig* – Die gierig-Stack- oder Schiebefenstertechnik ist ein häufiges Muster in Interviews (Arrays, Stacks, gierig). Es zeigt, dass Sie eine Reihe von Einschränkungen in eine optimale Reihenfolge in linearer Zeit übersetzen können.

---

oder 1. Problem Recap

> **Input**: ``s` – eine Zeichenfolge der Länge *n‐1*, jedes Zeichen ist entweder `'I'' oder `'D'`.
> **Ausgang**: die lexikographisch kleinste Permutation `perm` von `[1 ... n], die zufriedenstellt
> ` `
> s[i] == 'I' ‡ perm[i] < perm[i+1]
> s[i] == 'D'
> ` `

> **Beschränkungen*
> * 1 ≤ sLänge ≤ 105
> * s enthält nur `'I'' oder `'D'

> **Beispiel**
> `s = "DI" → `[2, 1, 3] ` (die kleinste unter `[2,1,3] und `[3,1,2] `)

---

oder 2. Die Greedy Insight

*Wenn wir die Zwänge für einen Moment ignorieren, ist die natürliche Ordnung `[1,2,3,...]` die lexikographisch kleinste Permutation. *

Ein Lauf von `'D'' zwingt eine ** abnehmende*** Folge.
In abnehmender Folge erhält man die kleinste lexicographische Permutation durch **reversing**, die laufen.

**Warum umkehrende Arbeiten* *
* Angenommen, wir haben einen Lauf `DI...I ` der Länge `k+1` beginnend bei index `i`.
* Die Zahlen, die Positionen besetzen `i ... i+k` sind die nächsten `k+1` natürlichen Zahlen: `i+1, i+2, ..., i+k+1`.
* Reversing gibt `i+k+1, ..., i+2, i+1`, das ist die kleinste Anordnung, die streng abnimmt.

So reduziert sich der gesamte Algorithmus auf:

`` `
prom = [1, 2, ..., n]
für jeden maximal aufeinanderfolgenden 'D'-Block [l ... r] in s:
Rückwärts perm[l] r+1
Rückkehr perm
`` `

Der Trick besteht darin, die Umkehr **in‐place* beim Scannen des Strings durchzuführen, wodurch ein expliziter Stack oder ein zusätzliches Array vermieden wird.

---

oder 3. Die drei mittelmäßigen Umsetzungen

Unten sind saubere, produktionsfertige Lösungen in Java, Python und C++.
Alle in `O(n)` Zeit laufen, verwenden Sie nur das Ausgabefeld als Hilfsraum (`O(1)` extra).

---

### 3.1 Java

``java
Import java.util.*;

Public class Lösung {\cHFFFF}
Int[] findPermutation(String s) {
int n = s.length() + 1;
int[] perm = neu int[n];

// Füllen Sie die natürliche Ordnung 1..n
für (in i = 0; i < n; ++i) perm[i] = i + 1;

int i = 0; // aktueller Index in s
(i < s.length() {\cHFFFF}
wenn (s.charAt(i) == 'I') { // nichts zu tun
i++;
weiter;
}

// wir haben einen D-Lauf getroffen. Das Ende finden
int start = i;
während (i < s.length() && s.charAt(i) == 'D') i++;

// Reverse perm[start ... i] (inklusive)
int links = start, rechts = i;
(links < rechts)
int tmp = perm[links];
perm[link] = perm[rechts];
perm[rechts] = tmp;
links++;
Rechts-
}
}

Rückgabe perm;
}

// Einfaches Testkabel
öffentliche statische Leerstelle (String[] args) {
System.out.println(Arrays.toString(
neue Lösung().findPermutation("DI")); // [2,1,3]
System.out.println(Arrays.toString(
neue Lösung().findPermutation("I")); // [1,2]
}
}
`` `

**Warum ist dies die “Gute” Java-Implementierung* *

| ✅ ✅ Feature |
|----------
| Einzelpass durch `s` | `O(n)` Zeit |
| Kein Hilfsstapel oder keine Liste ` `O(1)` |
| Klare Absicht: natürliche Füllung + selektive Umkehr | Einfach zu lesen und zu pflegen |

---

### 3.2 Python

```python
def find_permutation(s: str) -> list[int]:
n = len(s) + 1
perm = Liste(Bereich(1, n + 1)) # natürliche Bestellung

= 0
während i < len(s):
wenn s[i] == 'Ich':
= 1
weiter

Start = i
während i < len(s) und s[i] == 'D':
= 1

# reverse perm[start : i+1] in place
perm[start:i+1] = umgekehrt (prom[start:i+1])

Rückkehr perm

# Demonstranten
wenn __name__== "__main__":
Druck(find_permutation("DI") # [2, 1, 3]
Druck(find_permutation("I") # [1, 2]
`` `

Pythons Schichtauftrag mit `reversed()` gibt eine ein-liner Umkehr – die *Pythonic* Weg.

---

### 3.3 C++

```cpp
#include <bits/stdc++.h>
mit Namespace std;

Klasse Lösung {
öffentlich:
vektor<int> findPermutation(string s) {
int n = s.size() + 1;
Vektor<int> perm(n)
iota(prom.begin(), perm.end(), 1); // 1, 2, ..., n

int i = 0;
(i < (int)s.size() {\cHFFFF}
wenn (s[i] == 'I') { ++i; weiter; }

int start = i;
während (i < (int)s.size() &&s[i] == 'D' ++i;

// Reverse perm[start .. i]
umgekehrt (prom.begin() + start, perm.begin() + i + 1);
}
Rückgabe perm;
}
};

int main() {\cHFFFF}
Lösungssol;
auto res = sol.findPermutation("DI");
für (int x : res.)
cout << '\n';
}
`` `

C++ `iota` und `reverse` halten den Code terse und effizient.

---

oder 4. Das Gute, das Schlechte und die Ugly

| Stage | Was passiert | Wie zu vermeiden Schmerz |
-------------------------------------------------------
| **Das Gute** | Ein einziger linearer Pass, nur ganze Operationen, keine zusätzlichen Container. Verwenden Sie integrierte Helfer (`iota`, `reverse`, Scheibenzuweisung), um Code lesbar zu halten. |
| **The Bad** | Der Versuch, einen Stapel manuell zu bauen, führt zu **off‐by‐one** Fehlern und höheren konstanten Faktoren. Wenn Sie einen Stack benötigen, verwenden Sie ein `deque` oder `vector<int>` und pop/push vorsichtig. |
| **Die Ugly*** | Die "reverse" Logik innerhalb einer inneren Schleife, die auch das Array modifiziert, kann verwirrende geschachtelte Schleifen erstellen. | Die Logik trennen: 1) den Block `'D' identifizieren, 2) eine einzige Umkehr durchführen. 3) Weiter scannen. |

> **Interview Tip** – Wenn Sie jemals darum gebeten werden *erklären* diese Lösung, beginnen Sie mit dem Schreiben der natürlichen Ordnung, dann illustrieren, wie ein `D` Run eine Umkehr zwingt. Zeigen Sie ein schnelles Diagramm einer Sample-String: `D D I D` → `[1 2 3 4 5 6]` → Rückwärtspositionen 0‐2 → `[3 2 1 4 5 6] ` → weiter.

---

oder 5. Edge Cases & Komplexität

| Edge Case | Ergebnis |
|----------------------
| ``s` = `"I" | `[1, 2]` |
| ``s` = `"D" | `[2, 1]` |
| Alle `I`s | `[1, 2, ..., n]` |
| Alle `D`s | `[n, n-1, ..., 1]` |

**Komplexität* *

| Metric | Java | Python | C++ |
|------------------------
| Zeit | `O(n)` | `O(n)` | | `O(n)`` |
| Raum ` `O(1)` (Output-Array) | `O(1)` | | `O(1)` |

Die Eingabegröße constraint (105) wird bequem in allen drei Sprachen bearbeitet.

---

oder 6. Bonus – A Stack‐ Basierende Alternative (zur Diskussion)

Eine klassische "Stack"-Lösung drückt Indizes auf einen Stack, wenn ein "I''' oder das Ende der Strings gesehen wird, dann legt sie auf Werte.
Während noch `O(n)`, verwendet es einen zusätzlichen Stapel von Größe `O(n) ` und kann in der Praxis aufgrund des Speichers Overhead etwas langsamer sein.

``java
Stack<Integer> st = new Stack<>;
int val = 1;
für (in i = 0; i <= s.length(); i++)
st.push(i);
wenn (i == s.length() || s.charAt(i) == 'I') {
während (!st.isEmpty() perm[st.pop()] = val++;
}
}
`` `

Verwenden Sie dies nur, wenn Sie ausdrücklich aufgefordert werden, die Stack-Nutzung zu demonstrieren; ansonsten ist die Schiebefensterumkehr sauberer.

---

oder 7. SEO & Career‐Boosting Takeaway

ANHANG **Keywords** – *Leetcode 484, Finden Sie Permutation, gieriger Stack, lineare Zeit, Interview Problem, Java Python C++ Lösung, O(n) Algorithmus, Job Interview Codierung*
2. **Titel** – *“Master Leetcode 484: Finde Permutation – Greedy in Java, Python & C++”*
3. **Meta Beschreibung** – *Learn the schnellste way to lösen Leetcode 484, “Find Permutation”. Siehe Java-, Python- und C++-Implementierungen, Komplexitätsanalysen und behördliche Erklärungen. *

> **Warum ist das wichtig für Rekruten* Das Muster des Übersetzens einer Stringbeschränkung in eine Array-Bestellung ist eine häufige Interviewfrage für Software-Engineering-Rollen. Eine klare O(n)-Lösung in mehreren Sprachen zeigt Vielseitigkeit und algorithmische Grippe.

---

oder 8. Letzte Gedanken

* Halten Sie den Code **simple**: natürliche Ordnung + gezielte Umkehrungen.
* Testen Sie mit einigen handgefertigten Beispielen, insbesondere Randfällen.
* Wenn Sie in einem Interview diskutieren, gehen Sie durch das Beispiel auf einem Whiteboard und zeigen, wie jeder `'D'' ein Segment dreht.

Glückliche Kodierung – und viel Glück Landung, dass nächste Arbeit! 🚀