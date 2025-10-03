---
Titel: LeetCode 3158. Finden Sie den XOR der Zahlen, die zweimal erscheinen -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
3158. Finde den XOR der Zahlen, die zweimal erscheinen
** Schwierigkeit:** Easy | **Tags:** Array, Hash Table, Bit Manipulation

> **Problem**
> Sie erhalten ein ganzes Array `nums`. Jede Nummer im Array erscheint **once oder zweimal**.
> Geben Sie die Bitweise XOR von ** alle Zahlen zurück, die zweimal ** erscheinen. Wenn keine Nummer zweimal erscheint, `0` zurückgeben.

### Beispiel
| Eingabe | Ausgabe | Erklärung |
|-----------------------------
| `[1,2,1,3]` | `1` | Nur `1` erscheint zweimal. |
| `[1,2,3]`` | Keine Duplikate. |
| | `[1,2,2,1]` | `3` | `1 XOR 2 = 3` |

### Einschränkungen
- `1 ≤ nums.length ≤ 50`
- `1 ≤ nums[i] ≤ 50
- Jedes Element erscheint einmal oder zweimal.

---

Â ✅ Short & Efficient Solution (O(n) Zeit, O(n) Raum

Wir zählen die Frequenz jeder Zahl mit einem "HashMap" (oder einem Array der Größe 51, weil die Werte gebunden sind).
Während eines zweiten Passes XOR alle Tasten, die eine Frequenz von `2` haben.
Da XOR assoziativ ist, ist das Endergebnis der XOR aller Duplikatzahlen.

### Java
``java
java.util importieren. HashMap;
java.util importieren. Karte;

Klasse Lösung {
Int duplicateNumbersXOR(int[] nums) {
Karte<Integer, Integer> freq = new HashMap>();
für (int n : nums) {
freq.put(n, freq.getOrDefault(n) 0) + 1);
}

int xor = 0;
für (Map.Entry<Integer, Integer> e : freq.entrySet() {
wenn (e.getValue() == 2) xor ^= e.getKey();
}
zurück xor;
}
}
`` `

### Python
```python
aus Sammlungen Import Anzahl

Klasse Lösung:
def duplicateNumbersXOR(self, nums: List[int]) -> int:
freq = Zahl(nums)
Ergebnis = 0
für num, cnt in freq.items():
wenn cnt == 2:
^= num
Ergebnis
`` `

C++
```cpp
#include <bits/stdc++.h>
mit Namespace std;

Klasse Lösung {
öffentlich:
int duplicateNumbersXOR(vector<int& nums) {
unordered_map<int, int> freq;
für (int n : nums) freq[n]++;

int xor Val = 0;
für (auto &p : freq)
wenn 2) xorVal ^= p.first;
zurück xor Val;
}
};
`` `

---

Â 📖 Blog Artikel – “Das Gute, das Schlechte und die Ugly” von LeetCodes *Find the XOR of Numbers, die zweimal erscheinen*

### Meta Beschreibung
> Master LeetCodes „Find the XOR of Numbers, die zweimal erscheinen“ mit einer sauberen O(n)-Lösung in Java, Python und C++. Lernen Sie die Profis, Fallstricke und interviewfreundliche Tricks, um dieses einfache Problem zu lösen und Ihre nächste Tech-Rolle zu landen.

---

### Inhaltsverzeichnis
ANHANG [Problemübersicht](#Problem-Übersicht)
2. [Warum XOR?](#why-xor)
3. [Solution Walk‐through](#solution-walk-through)
4. **Das Gute** – Clean, Linear-time Algorithmus
5. **The Bad** – Randfälle und Über-Engineering
6. **The Ugly** – Häufige Fehler und Leistungsfalle
7. [Alternate Ansätze](#alternate-approaches)
8. [Test & Edge‐Case Checklist](#testing)
9. [SEO & Interview Tipps](#seo-interview-tips)
10. [Abschluss](#Abschluss)

---

oder 1. Problemübersicht <a name="Problemüberblick">/a>
LeetCode's *Find the XOR of Numbers Welches Aussehen Twice* ist ein **easy*-Array-Problem, das testet:

- Frequenzzählung
- Bitwise XOR Eigenschaften
- Effiziente Verwendung von Hash-Strukturen

Weil die Zahlen klein sind (` ≤ 50`) können wir sogar eine Hash-Karte durch ein fest-size-Array ersetzen, aber eine Hash-Karte hält den Code generisch.

---

oder 2. Warum XOR? <a name="why-xor">/a>
XOR ist eine perfekte Passform für dieses Problem:

| Immobilien | Warum es hilft |
|--------------------------
| **XOR identischer Zahlen ist 0** | `x ^ x = 0` – Duplikate löschen sich gegenseitig aus. |
| **XOR ist assoziativ und kommutativ** | Bestellen spielt keine Rolle – wir können Ergebnisse in jedem Pass sammeln. |
| **XOR von `0` mit einer Nummer ist, dass Nummer** | Ab `0` ist natürlich. |

Diese Eigenschaften lassen uns *sammeln* Duplikate effizient, ohne Sortieren oder Nistschleifen.

---

oder 3. Lösung Walk‐through <a name="solution-walkthrough">/a>
ANHANG ** Frequenzen** Ein Linearpass mit Hash-Karte oder Zählfeld.
2. **XOR Duplikate** – Zweiter Pass: XOR nur die Zahlen, deren Anzahl genau `2` ist.
3. **Return** – Wenn keine Duplikate gefunden wurden, bleibt `xor` `0` (die richtige Antwort).

*Zeitkomplexität:* **O(n)* – ein oder zwei Übergänge über das Array.
*Space-Komplexität:* **O(n)** – Hash-Kartengröße proportional zu verschiedenen Elementen (≤ 50).

---

oder 4. Das Gute <a name="thegood">/a>
| Aspect | Warum es gut ist |
|--------------------------
| **Simplicity** – Zwei klare Schleifen; keine versteckte Logik. |
| **Deterministisch** – Arbeitet für alle Inputs in Zwängen. |
| **Skalierbar** – Wenn Zwänge wachsen (z.B. `nums.length = 106`), skaliert der Algorithmus noch linear. |
| **Language‐agnostic* – Implementierung in Java, Python, C++ mit minimalen Änderungen. |
| **Interview-freundlich** – Zeigt Wissen über Hashtabellen und bitweise Ops, beide gemeinsamen Interview-Themen. |

---

oder 5. The Bad <a name="the-bad">/a>
| Pitfall | Remedy |
|----------------------
| **Angenommen, alle Duplikate sind genau 2** – Problem garantiert es, aber in realen Daten können Sie Triplikate sehen. | Gültige Eingabe oder Addition von Behauptungen. |
| ** Die Verwendung schwerer Datenstrukturen* – Ein voller `HashMap` ist übertötet für kleine `nums`. | Ersetzen mit einem festen 51-Element-Array (`int[51]`). |
| **Nicht mit leerem Array** – Nicht benötigt für LeetCode, sondern gute Praxis. | Return `0` oder eine Ausnahme erhöhen, wenn `nums.isEmpty()`. |

---

oder 6. Der Ugly <a name="the-ugly">/a>
| Fehler | Auswirkung | Fix |
|--------------------------
| **Brute Kraft-Doppelschleife* – `O(n2)` Zeit. | TLE auf größeren Eingaben (auch wenn versteckte Tests über Einschränkungen hinausgehen). | Verwenden Sie Hash-Karte oder Frequenz-Array. |
| ** Verwenden von `Set` zum Detektieren von Duplikaten* – `O(n)`, aber Sie müssen immer noch alle Duplikate XOR. | Misses Duplikate erscheinen zweimal, wenn Sie nur Präsenz überprüfen. | Store zählt, nicht nur Präsenz. |
| **Relying auf bitweise Magie ohne Erklärung** Interviewer können *Warum* Sie verwendet XOR. | Risiko als „Black‐box-Codeer“ gesehen zu werden. | Erklären Sie kurz XOR-Eigenschaften in Ihrer Erklärung. |
| **Ignorieren ganzzahliger Überlauf** – XOR überlauft nicht, aber das Hinzufügen von Frequenzen könnte, wenn Sie `int` für große Zählungen verwenden. | Selten für Zwänge, aber eine gute Gewohnheit zu verwenden `long`. | Verwenden Sie `int` für Zählungen, wenn max bekannt ist, andernfalls verwenden `long`. |

---

oder 7. Alternate Approaches <a name="alternate-approaches">/a>

ANHANG **Counting Array** (seit Werten ≤ 50):
``java
int[] freq = neu int[51];
für (int n : nums) freq[n]++;
int xor = 0;
für (int i = 1; i <= 50; i++) wenn (freq[i] == 2) xor ^= i;
`` `

2. **Bit Manipulation ohne Hash**
Für jede Bitposition `b` (0..31) zählen, wie viele Zahlen Bit `b` gesetzt haben.
Wenn ein bisschen über Duplikate eine gleichmäßige Anzahl von Zeiten erscheint, bricht es aus.
Dies ist komplexer und für die gegebenen Zwänge nicht erforderlich.

3. **Sortung + Scan**
Sortieren Sie das Array (O(n log n)) und scannen Sie einmal für Paare.
Nicht so effizient wie O(n) Zählen, sondern einfacher zu kodieren in Sprachen ohne Hash-Tabellen.

---

oder 8. Test & Edge‐Case Checklist <a name="test">/a>
| Test | Input | Erwartete Ausgabe |
---------------------------------
| Alle einzigartigen | `[1,2,3,4]` | `0` |
| Alle Duplikate | `[5,5,5,5]` (ungültig nach Zwängen) | N/A |
| Ein Duplikat | `[10,20,10]` | `10` |
| Mehrere Duplikate | `[1,2,1,3,3]` | `0` (1^2^3 = 0) |
| Boundary Werte | `[50,50]` | `50` |
| Gemischte Reihenfolge | `[3,1,2,3,2,1]` | `0` |

---

oder 9. SEO & Interview Tipps <a name="seo-interview-tips">>/a>
| Fokus | Warum es Materie |
|--------------------------
| **Keywords** – „LeetCode XOR Problem“, „findet XOR doppelter Zahlen“, „Java Bit Manipulation Interview“ | Erhöht Suchverkehr und Sichtbarkeit der Rekrutierer. |
| **Clear Code Blocks* – Separate Sprachabschnitte, Füge Kommentare | Ermöglicht den Artikel auf GitHub, StackOverflow und Codierung von Blogs. |
| **Interview Insight** – Diskutiert Trade‐offs, Zeit/Raum-Komplexität | Zeigt Tiefe, ein Muss für ältere Rollen. |
| **Result‐orientiert** – Erwähnung „runs in O(n) time“ und „Handles edge cases“ | Recruiters suchen nach effizienten Lösungen. |
| **Call to Action** – “Try this on LeetCode, senden und verfolgen Sie Ihre Bewertung” | Engages Leser und steigert Engagement Metriken. |

---

oder 10. Fazit < a name="conclusion">/a>
LeetCode's *Find the XOR of Numbers Welche Appear Twice* ist eine schnelle Sanitätsprüfung für Ihre Fähigkeit, Zählen mit bitweise Operationen zu kombinieren.
Durch die Verwendung einer Frequenzkarte (oder Array) und die Nutzung der Eigenschaften von XOR können Sie das Problem in linearer Zeit mit minimalem Code lösen – genau die Art der sauberen, effizienten Lösung Interviewer lieben.

Probieren Sie es auf der Plattform LeetCode, fügen Sie ein paar Einzeltests hinzu und vergessen Sie nicht, Ihren Ansatz in Ihrem Portfolio zu dokumentieren. Eine solide, interview-ready Lösung wie diese kann der Unterschied zwischen der Landung eines Gesprächsgesprächs und dem unbemerkten gehen. Glückliche Kodierung!

---

### 📌 Final Code Snippets (Copy‐Paste Ready)

oder Java
``java
java.util importieren. HashMap;
java.util importieren. Karte;

Public class Lösung {\cHFFFF}
Int duplicateNumbersXOR(int[] nums) {
Karte<Integer, Integer> freq = new HashMap>();
für (int n : nums) freq.put(n, freq.getOrDefault(n, 0) + 1);

int xor = 0;
für (var Eintrag : freq.entrySet())
wenn (entry.getValue() == 2) xor ^= Eintrag.getKey();

zurück xor;
}
}
`` `

Python
```python
aus Sammlungen Import Anzahl
aus der Einfuhr Liste

Klasse Lösung:
def duplicateNumbersXOR(self, nums: List[int]) -> int:
freq = Zahl(nums)
Ergebnis = 0
für num, cnt in freq.items():
wenn cnt == 2:
^= num
Ergebnis
`` `

C++
```cpp
#include <bits/stdc++.h>
mit Namespace std;

Klasse Lösung {
öffentlich:
int duplicateNumbersXOR(vector<int& nums) {
unordered_map<int,int> freq;
für (int n : nums) ++freq[n];

int xor Val = 0;
für (auto &p : freq)
wenn 2) xorVal ^= p.first;

zurück xor Val;
}
};
`` `

Glückliche Lösung, und viel Glück Landung dieser Tech-Job!