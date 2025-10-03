---
Titel: LeetCode 3528. Unit Conversion Ich...
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
oder 1. Lösungscode

Im Folgenden finden Sie **drei vollverarbeitende, produktionsfertige** Lösungen für LeetCode 3528 – Umrechnung I.
Jede Lösung läuft in **O(n)*-Zeit und **O(n)**-Speicher, einfach mit den Grenzen (`n ≤ 105`, `Faktor ≤ 109`).

| Sprache | Schlüsselidee | Komplexität |
------------------------
| **Java** | Iterative DFS auf einem gerichteten Baum (root 0) – Produktmodulo *M* | **O(n)** Zeit, **O(n)** Speicher |
| **Python** | Iterative DFS / Stack – Produktmodul *M* | **O(n)* Zeit, **O(n)* Speicher |
| **C++** | Stapelbasierte DFS – Produktmodul *M* | **O(n)** Zeit, **O(n)** Speicher |

> **HINWEIS**
> Das Problem garantiert, dass `conversions` einen **directed tree rooted at 0** (einziger Pfad von 0 zu jedem Knoten) bilden.
> Eine einfache Tiefenausbreitung des Produktes ist daher ausreichend – kein Bedarf an BFS oder Dijkstra.

---

### 1.1 Java – `Solution.java `

``java
Import java.util.*;

Public class Lösung {\cHFFFF}
private statische Endstufe MOD = 1_000_000_007;

Public int[] baseUnitConversions(int[][] Conversions) {
int n = Umrechnungen.Länge + 1;
List<int[]>[] graph = new ArrayList[n];
für (int i = 0; i < n; i++) graph[i] = new ArrayList<>();

// Erstellen Sie die gerichtete Anzeigeliste
für (int[] e : Conversions) {\cHFFFF}
int src = e[0], tgt = e[1], Faktor = e[2];
graph[src].add(new int[]{tgt, Factor});
}

lang[] ans = neu lang[n];
ans[0] = 1L; // 1 Einheit des Typs 0 gleich 1 Einheit des Typs 0
Deque<Integer> Stack = new ArrayDeque<>>;
Stack.push(0);

während (!stack.isEmpty() {\cHFFFF}
int u = Stack.pop();
für (int[] edge : graph[u]) {\cHFFFF}
int v = Rand[0];
Länge f = Kante[1];
ans[v] = (ans[u] * f) % MOD;
Stack.push(v)
}
}

// Int-Array umrechnen, bevor Sie zurückgeben
Int[] Ergebnis = neuer Int[n];
für (int i = 0; i < n; i++) Ergebnis[i] = (int) ans[i];
Rückgabeergebnis;
}
}
`` `

---

### 1.2 Python – `solution.py `

```python
aus der Einfuhr Liste

MOD = 10**9 + 7

Klasse Lösung:
def base UnitConversions(self, Conversions: List[List[int]]) -> Liste[int]:
n = len(Konversionen) + 1
g = [[] für _ im Bereich(n)]
für src, tgt, f in Umrechnungen:
g[src].append((tgt, f))

as = [0]
ans[0] = 1
Stapel = [0]

während des Stapels:
u = Stack.pop()
für v, f in g[u]:
ans[v] = (ans[u] * f) % MOD
Stack.append(v)

Rückgabe an
`` `

---

### 1.3 C++ – `solution.cpp `

```cpp
#include <bits/stdc++.h>
mit Namespace std;

Klasse Lösung {
öffentlich:
statischer Kegel int MOD = 1'000'000'007;

vektor<int> baseUnitConversions(vector<vector< in>>& Conversions) {\cHFFFF}
int n = Conversions.size() + 1;
Vektor<vector<pair<int, lang>>> g(n)
für (Auto &e : Umrechnungen) {\cHFFFF}
int src = e[0], tgt = e[1];
Länge f = e[2];
g[src].push_back({tgt, f});
}

Vektor<long long> ans(n, 0)
as[0] = 1
Stack<int> st;
st.push(0);

während (!st.empty() {\cHFFFF}
int u = st.top(); st.pop();
für (auto &p : g[u]) {\cHFFFF}
int v = p.first;
lang f = p.Sekunde;
ans[v] = (ans[u] * f) % MOD;
st.push(v)
}
}

Vektor<int> res(n)
für (int i = 0; i < n; ++i) res[i] = static_cast<int>(ans[i];
zurück;
}
};
`` `

Alle drei Implementierungen verwenden **iterative DFS** (Stack), um Stapelüberlauf für tiefe Bäume (bis zu 100 000 Knoten) zu vermeiden.
Sie propagieren das Produkt von Konversionsfaktoren von der Wurzel (Einheit 0) zu jedem anderen Knoten, wobei der Modulo `1 000 000 007 ` wie erforderlich.

---

oder 2. Blog Artikel – „Unit Conversion I on LeetCode: The Good, The Bad, and The Ugly“

> **SEO Keywords:** *LeetCode 3528*, *Unit Conversion*, *Java Lösung*, *Python Lösung*, *C++ Lösung*, *DFS*, *BFS*, *Grafikbaum*, *Coding Interview*, *job interview*, *algorithm analysis*, *software engineer interview*, *coding interview Questions*

---

### 2.1 Einführung

Wenn Sie für ein Software-Engineering-Interview vorschlagen, ist der LeetCode Problemsatz Ihr Spielplatz. Unter den vielen „mittleren“ Herausforderungen steht **Unit Conversion I (LeetCode 3528)***: Es testet Graphentraversal, modular arithmetic und die Fähigkeit, versteckte Struktur in der Eingabe zu erkennen.

In diesem Beitrag deaktivieren wir das Problem, gehen durch die elegantsten Lösungen in **Java, Python und C++** und diskutieren:

**The Good** – warum das Problem eine große Interviewfrage ist
**The Bad** – häufige Fallstricke, die Reisekandidaten
* **The Ugly** – Kanten-Fall-Nuancen, die Ihren Code still brechen können

Am Ende haben Sie eine produktionsbereite Lösung und eine klare Erzählung, um mit Interviewern zu teilen.

---

### 2.2 Problem Recap

Sie erhalten `n` Einheitstypen (0 ... n‐1) und ein Array `conversions` der Länge `n-1`.
Jedes Element `conversions[i] = [Quelle, Ziel, Faktor]` bedeutet *1 Einheit von `source` gleich `factor` Einheiten von `target`*.

**Goal:** Für jeden Typ `i` berechnen Sie, wie viele Einheiten des Typs `i` entsprechen * eine* Einheit des Typs `0`. Rückgabe der Ergebnisse modulo `1 000 000 007`.

**Beschränkungen* *

`2 ≤ n ≤ 105`
* `1 ≤ Faktor ≤ 109 `
* Der Graph ist ein **geleiteter Baum, der bei 0** verwurzelt ist (einziger Pfad von 0 zu jedem Knoten).
* Die Antwort kann riesig sein, so ist Modulo `MOD = 1 000 000 007` obligatorisch.

---

### 2.3 Die versteckte Struktur entdecken – Das Gute

Das Problem sieht aus wie ein generisches "gewichtetes Diagramm" Problem, aber die zusätzliche Linie in den Zwängen ist ein *goldenes Ticket*:

> * Es ist gewährleistet, dass die Einheit 0 durch eine einzigartige Kombination von Konvertierungen in jede andere Einheit umgewandelt werden kann. *

Das bedeutet, dass die Eingabe tatsächlich ein **geleiteter Baum** ist (keine Zyklen, keine Verzweigung von der Wurzel zurück zu sich). In der Graphentheorie sind Bäume die einfachsten verbundenen Strukturen. Sobald Sie dies erkennen, reduziert sich das ganze Problem auf eine einzelne DFS/BFS, die die Kantengewichte entlang des einzigartigen Pfades multipliziert.

Warum ist das eine gute Interview-Einsicht?

ANHANG **Zeitsparen** – Sie vermeiden generische Kurzwegalgorithmen (Dijkstra, Bellman‐Ford), die sonst übertrieben werden.
2. **Klarität** – eine klare Problemerklärung → eine klare Lösungsstrategie → ein zuversichtliches Interview.
3. **Optimierung** – Sie können einen *O(n)* Algorithmus implementieren, der bequem in 1 s Zeitlimit passt.

---

### 2.4 The Algorithm – DFS Propagation

**Kernidee**
Ausgehend von der Wurzel (Einheit 0) durchqueren Sie den Baum.
Für jede Kante `u → v` mit Gewicht `w`, propagate

`` `
Wert[v] = Wert[u] * w mod MOD
`` `

Da der Pfad von 0 zu jedem Knoten einzigartig ist, gibt es keine Notwendigkeit für "best‐path" Logik oder Prioritäts-Warteschlangen.

**Einführungsdetails*

| Schritt | Was zu tun | Warum es wichtig ist |
---------------------------------------
| Adjacency List erstellen | `List<int[]>[] g = new ArrayList[n]; | Fast Nachbar Lookup (`O(1)` pro Kante). |
| Verwenden Sie einen iterativen Stack/queue | `Deque<Integer> Stack = new ArrayDeque>>(); | Vermeidet Recursion Tiefengrenzen (100 000 Knoten). |
| Behalten Sie `long` Zwischenwerte | `long val = ans[u] * w % MOD; | `factor` kann bis zu `109` sein; Produkt kann `int` überlaufen. |
| Return `int[]` | Konvertieren Sie die `long[] ans` in `int[]`, bevor Sie die Signatur von | LeetCode zurückgeben, erfordert `int[]`. |

> **BFS vs. DFS*
> Beide sind in Ordnung. DFS (Stack) ist ein wenig speicherfreundlicher für Bäume, da Sie nur die Elternwerte speichern müssen. BFS (queue) würde dasselbe mit im Wesentlichen dem gleichen Overhead tun.

---

### 2.5 Code Walkthrough – The Ugly Edge Cases

| Sprache | Gemeinsamer Fehler | Fix |
------------------------------------
| **Java*** | Rückgabe `long[]` direkt | LeetCode erwartet `int[]`. Die Endumsetzung ist obligatorisch. |
| **Python** | Verwenden von `stack = [0] und `stack.pop()` | Werke, aber ein `deque` gibt etwas bessere Leistung für große n. |
| **C++** | Verwenden von `int` für Gewichte | Konvertieren zu `long long` vor der Multiplikation. |

oder Rand Fall 1: Modulo „Zero“
Wenn `Faktor` ein Vielfaches von `MOD` ist, wird `Faktor % MOD` 0 und propagiert nachgeschaltete Nullen. Das ist *Korrekt*, weil modulo arithmetic sich so verhält. Stellen Sie sicher, dass Sie den Modulo **nach* jede Multiplikation anwenden, nicht nur am Ende.

oder Rand Fall 2: Überlauf auf 32-Bit-Integer
`1 000 000 007 × 109` überschreitet den 32-Bit-unterzeichneten Ganzzahlbereich (`≈ 2.1 x 109`).
Die Verwendung von `long` (64‐bit) für das Zwischenprodukt und dann `mod` garantiert Richtigkeit.

oder Rand Fall 3: Stack Size in Recursion
Eine naive rekursive DFS kann den JVM/CPython/C++ Call Stack auf einen tiefen Baum sprengen. Mit einem expliziten Stack (`ArrayDeque` / `std::stack`) ist ein *must*.

---

### 2.5 Komplexitätsanalyse

| Algorithm | Zeit | Raum |
|---------------------
| Iterative DFS | **O(n)** (jeder Knoten & Rand einmal besucht) | **O(n)** (Grafik + Antwort-Array) |
| BFS / queue | Gleich wie DFS | Gleiches |
| Generische Dijkstra (wenn Sie die Baumeigenschaft ignorieren) | **O(n log n)** | **O(n)***

Die optimale Lösung ist die einfachste und schnellste Lösung und bietet Ihnen einen **10-Punkt-Vorteil** im Interview.

---

### 2.6 Interview‐ Fertige Tipps

ANHANG **Erklären Sie das Baumeigentum zuerst** – fragen Sie den Interviewer, ob die Grafik garantiert ein Baum ist. Es zeigt, dass Sie nach versteckten Einschränkungen suchen.
2. **Clarify the modulo Operation** – stellen Sie sicher, dass der Interviewer weiß, dass Sie `mod` bei * jeder Multiplikation* nehmen, nicht nur die endgültige Antwort.
3. **Discuss Stack vs recursion** – erwähnen, warum ein iterativer Ansatz für LeetCodes 100 000 Limit sicherer ist.
4. **Zeigen Sie den Code in mehreren Sprachen** – Sie können sagen: "Ich habe eine saubere, O(n) DFS in Java/Python/C++" und fallen die Schnipsel als Handout.

---

### 2.7 Was der Recruiter wird bemerken

* **Pattern Recognition** – die Baumstruktur zu erkennen ist ein Kennzeichen eines erfahrenen Kodierers.
* **Attention to Detail** – Umgang mit dem Modul korrekt, mit `long`, um Überlauf zu vermeiden, und die Wahl einer iterativen Traversal alle demonstrieren produktionsbereite Codierung.
* **Kommunikation** – Schritt für Schritt durch den Algorithmus zeigt, dass Sie komplexe Ideen einfach erklären können – eine kritische Soft-Skill für Senior-Rollen.

---

### 2.8 Bonus: Wie man dieses Problem für eine „Real‐World“-Pitch verwendet

Wenn Sie sich für eine **Backend Engineer** oder **Systems Engineer** Rolle bewerben, können Sie Ihre Lösung als „Modular Conversion Engine“ rahmen.
* „Ich habe ein leichtes baumbasiertes Ausbreitungssystem aufgebaut, das auf willkürlich gerichtete Grafiken erweitert werden kann. „
* „Das modulare arithmetische Muster, das ich hier verwendete, ist genau das, was wir in tokenbasierten Zugangskontrollen einsetzen. „

Diese Verbindungen helfen Ihnen, ein Codierungsproblem in eine **-Story über Architektur** zu verwandeln, die Manager lieben.

---

### 2.9 Letzte Gedanken

Umrechnung von Einheiten Ich bin trügerisch einfach, wenn Sie die Zwänge sorgfältig lesen.
Eine saubere DFS/BFS, die Gewichte entlang eines Baumes multipliziert, ist die *optimale* Strategie.
Mit den drei Codemustern oben, Sie sind bereit, jeden Interviewer zu beeindrucken – ob sie nach **Java**, **Python*, oder **C++*****.

> **Weitere Schritte*
> 1. Führen Sie die Lösungen auf LeetCodes Testkabel.
> 2. Fügen Sie sie zu Ihrem persönlichen “interview cheat Blatt. „
> 3. Praxis zur Erläuterung der Baumeigenschaft und des Verbreitungsalgorithmus – die häufigste Frage wird *“Warum haben Sie DFS über Dijkstra gewählt?”*

Viel Glück und kann Ihr Interview so glatt wie ein perfekt ausgeglichener Baum sein!

---

### 2.10 TL;DR

| Was Sie lernen 🎯 🎯 Wer es hilft |
-------------------------
| Tree-Erkennung in Graph-Problemen | **Interviewers* – zeigt Einblick |
| O(n) DFS-Vermehrung mit Modulo | **Candidates** – einfach zu codieren, schnell |
| Production‐ready Java/Python/C++ code | **All* – copy‐paste in your IDE |

Lassen Sie diese Schnipsel in Ihr Portfolio fallen, führen Sie sie gegen die LeetCode-Tests und bringen Sie das **-Story** von "dem versteckten Baum" in Ihr nächstes Interview. Viel Glück – und genießen Sie die Umwandlung von Zeit in Interview gewinnt!