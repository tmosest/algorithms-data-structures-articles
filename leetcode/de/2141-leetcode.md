---
Titel: LeetCode 2141. Maximale Laufzeit von N Computern -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
Lösungsübersicht – LeetCode 2141: Maximale Laufzeit von N Computern

**Problemerklärung* *
Sie haben `n` Computer und ein Array `Batterien`.
`Batterien[i]` ist die Anzahl der Minuten, die eine einzelne Batterie einen Computer antreiben kann.
In jeder ganzzahligen Minute können Sie Batterien zwischen Computern wechseln (Swapping dauert keine Zeit).
Ihr Ziel ist es, alle `n` Computer ** simultan** für möglichst viele Minuten zu betreiben.
Gibt die maximale Anzahl von Minuten zurück.

> **Beschränkungen*
> * `1 ≤ n ≤ Batterien.Länge ≤ 10^5 `
> * `1 ≤ Batterien[i] ≤ 10^9

Die wichtigsten Erkenntnisse:
In jedem Intervall der Länge `T`, *je* Batterie kann höchstens `T` Minuten Leistung beitragen, auch wenn es länger laufen könnte.
Somit beträgt der Gesamtbeitrag aller Batterien zu einem `T`‐Minutenlauf höchstens `min(Batterie, T)` für jede Batterie.

Wir präsentieren zwei beliebte Ansätze, beide mit einer Zeitkomplexität von `O(m log m)`` `m = Batterien.Länge `.
Das **sort‐and‐trim*-Verfahren ist einfacher zu verstehen und umzusetzen, während die **binäre Suche**-Methode etwas „algorithmischer“ ist und einen anderen Winkel zeigt.

Im Folgenden finden Sie in **Java**, **Python** und **C++** fertige Implementierungen.

---

Sort‐and‐Trim Lösung (O(m log m))

Die Idee ist, alle Batterien zu halten, außer die, die “verschwendet” wäre, wenn sie zu mächtig im Vergleich zur aktuellen durchschnittlichen Laufzeit sind.

ANHANG **Sort*** das Batteriefeld.
2. Berechnung der Gesamtenergie `sum`.
3. Beginnend von der größten Batterie, entfernen Sie es von der Überlegung, während es größer ist als der aktuelle durchschnittliche `sum / (n - k)`.
*Wenn eine Batterie entfernt wird, reduzieren wir `sum` und `n` um eins. *
4. Nach dem Trimmen ist die Antwort einfach `sum / n` (Integer Division – alles passt jetzt perfekt).

### Warum es funktioniert

- Ja. Wenn die stärkste Batterie mehr Leistung als der Durchschnitt hat (`sum / n`), würde sie allein für diese durchschnittliche Zeit verwendet werden und der Rest der Batterien wäre leer.
Entfernen Sie es und Berücksichtigung des Durchschnitts gibt eine engere gebunden.
- Ja. Wir machen das solange, bis die stärkste verbleibende Batterie die Last mit den übrigen Batterien teilen kann, ohne Energie zu verschwenden.
An dieser Stelle kann jede Batterie für genau `sum / n` Minuten verwendet werden, was optimal ist.

---

🧪 2️⃣ Binäre Suchlösung (O(m Logsumme))

Alternative aber ebenso schnelle Annäherung:

ANHANG Die Gesamtenergie `total` berechnen.
2. Setzen Sie `low = 0`, `high = total / n`. (Kein Lauf kann diese obere Grenze überschreiten.)
3. Während `low ≤ high`:
* Überprüfen Sie, ob ein Lauf von `mid` Minuten möglich ist.
* Wenn ja, speichern Sie es und suchen Sie höher; sonst suchen Sie tiefer.
4. Um ***** einen Kandidaten `mid`:
* Jede Batterie trägt `min(Batterie, Mitte)` Minuten bei.
* Summe aller Beiträge; wenn die Summe mindestens `n * mid` ist, ist der Lauf möglich.

Beide Ansätze sind `O(m log m)`, aber die binäre-search-Version verwendet nur einen einzigen Pass über das Array pro Iteration.

---

📄 3️⃣ Code Implementierungen

Unten sind saubere, kommentierte Lösungen in drei Sprachen.
Alle verwenden 64-Bit arithmetic (`long` / `long long`), da die Gesamtsumme 32 Bit überschreiten kann.

### Java

``java
java.util importieren. Strahlen;

Public class Lösung {\cHFFFF}
/**
* Geben Sie die maximale Anzahl von Minuten alle `n` Computer können gleichzeitig laufen.
* @param n Anzahl der Computer
* @param Batterien Anzahl der Akkulaufzeiten
* @Return maximale gleichzeitige Laufzeit (Minuten)
*
Public long maxRunTime(int n, int[] Batterien) {\cHFFFF}
Arrays.sort(Batterien); // O(m log m)

lange Summe = 0;
für (int b : Batterien) Summe += b; // Gesamtenergie

int idx = Batterien.Länge - 1; // Start vom größten
während (idx >= 0 && Batterien [idx] > Summe / n) {\cHFFFF}
sum -= Batterien[idx]; // zu leistungsfähige Batterie entfernen
idx--; // Schrumpfen Sie das nutzbare Array
n--; // ein weniger Computer
}

Rückgabesumme / n; // endgültige Antwort
}
}
`` `

### Python

```python
def maxRunTime(n: int, Batterien: list[int]) -> int:
""
Gibt die maximale Anzahl von Minuten alle `n` Computer können gleichzeitig laufen.
""
Batterien.sort() # O(m log m)

Gesamt = Summe (Batterien)
i = len(Batterien) - 1 # Index der größten Batterie

# Trim Batterien, die verschwendet würden
während i >= 0 und Batterien[i] > insgesamt // n:
Gesamt -= Batterien[i]
i) = 1
-= 1

insgesamt // n
`` `

C++

```cpp
#include <bits/stdc++.h>
mit Namespace std;

Klasse Lösung {
öffentlich:
lange maxRunTime(int n, vector<int>>& Batterien) {\cHFFFF}
sort(batterien.begin(), Batterien.end()); // O(m log m)

lange lange Summe = 0;
für (int b : Batterien) Summe += b; // Gesamtenergie

int idx = Batterien.size() - 1;
während (idx >= 0 && Batterien [idx] > Summe / n) {\cHFFFF}
sum -= Batterien[idx]; // zu stark entfernen
idx--
n--
}
Rückgabesumme / n;
}
};
`` `

---

📚 4️⃣ Blog Artikel – “Das Gute, das Schlechte und die Ugly von LeetCode 2141”

> **Titel***: *Mastering LeetCode 2141 – Maximale Laufzeit von N Computern*
> **Meta‐Beschreibung*: Entdecken Sie die optimale Lösung, Fallstricke und befragungsreife Einblicke für LeetCode 2141. Lesen Sie den vollständigen Leitfaden in Java, Python und C++.

---

### 1. Einleitung

LeetCode 2141 bittet Sie, die gleichzeitige Laufzeit einer Reihe von Computern mit einem Pool von Batterien zu maximieren.
Es ist ein klassisches *Resource‐allocation* Problem, das häufig in technischen Interviews erscheint.
Warum? Weil es Sie dazu zwingt, über **Kapazitätsplanung*, **greedy trimming* und **binary search** nachzudenken – alle Fähigkeiten, die für daten-engineering und Backend-Rollen hochwertig sind.

### 2. Problem Recap

Sie haben:
- Computer.
- `m = Batterien.Länge` Batterien.
- `Batterien[i]` = Laufzeit der Batterie `i` (Minuten).

Sie können Batterien zwischen Computern jederzeit wechseln (Swapping ist sofort).
Ziel: die maximale Anzahl von Minuten finden alle `n` Computer können ** simultan** laufen.

### 3. Intuition & Hauptbeobachtungen

| Beobachtung | Warum es wichtig ist |
|-------------------------
| **O(1) Swap** | Erlaubt Ihnen, sofort wieder auszubalancieren; die einzige reale Beschränkung ist die Batteriekapazität. |
| **Batterie kann T** | Während eines `T`‐Minuten-Intervalls nicht überschreiten, trägt eine Batterie höchstens `T` Minuten bei. |
| **Gebäude Gesamt** | Ein Lauf der Länge `T` ist machbar iff `Σ min(battery, T) ≥ n * T`.

Die letzte Beobachtung gibt uns eine **Entscheidung Funktion* – ein perfekter Kandidat für binäre Suche.

### 4. Das Gute – Sort‐and‐Trim

oder Was es tut

ANHANG Batterien aufsteigen.
2. Beschneiden Sie die stärkste Batterie, wenn es sonst "Idee" wäre.
3. Die restlichen Batterien können alle für genau `sum / n` Minuten verwendet werden.

Warum es gut ist

- **Einfach zu erklären** – perfekt für ein Interview.
- **Fast** – ein `O(m log m)` sort + ein einziger linearer Scan.
- **Deterministisch** – keine zufälligen Faktoren; immer die gleiche Antwort für die gleiche Eingabe.

Code‐Snippet (Java)

``java
Arrays.sort(Batterien);
während (Batterien [idx] > Summe / n) { ... }
`` `

### 5. Das Böse – Binary Search Pitfalls

Binäre Suche ist elegant, aber subtil:

- **Wrong obere gebunden** → unendliche Schleife.
Verwenden Sie immer `high = total / n`, nicht `total` selbst.
- **Integer Division** – `mid = (niedrig + hoch) / 2` kann überlaufen; verwenden `low + (hoch - niedrig) / 2`.
- **Feasibility Funktion** – Sie müssen `min(battery, mid) ` zusammenfassen; Vergessen Sie die Kappe bei `mid` wird falsche Ergebnisse geben.

Interview‐Ready Tip
Wenn Sie gebeten werden, die binäre Suche zu rechtfertigen, markieren Sie, dass `mid` eine **guess** für die Ziellaufzeit ist, und der Machbarkeitstest ist im Wesentlichen ein *knapsack* mit gebundenen Gewichten.

### 6. Die Ugly – Common Traps & Edge Cases

| Fallbeispiel | Fix |
|------------------------
| **32‐bit Overflow** | `sum` von 10^5 Batterien je 10^9 = 10^14 | Verwenden Sie `long` / `long long`. |
| **Empty Battery List** | `m < n` | Problemgarantien `m ≥ n`; noch, Wache gegen Division durch Null. |
| **Alle Batterien gleich** | `Batterien = [5,5,5]` | Nach Sortierung läuft die Trimmschleife nicht; Antwort ist `15/3 = 5`. |
| **Sehr starke Batterie** | `[1000,1,1]`, `n=2` | Trim 1000 → `sum=2`, `n=2`, Antwort `1`. |

### 7. Komplexitätsanalyse

| Approach | Zeit | Raum |
|-------------------------
| Sortieren Trim | `O(m log m)` | `O(1)`` |
| Binary Search | `O(m log (total / n)` | `O(1)` |

Mit `m ≤ 10^5` sind beide gut in den Grenzen von LeetCode.

### 8. Interview Tipps

- **Erklären Sie die Entscheidungsfunktion** vor der Kodierung; Interviewer lieben es, Ihren Gedankenprozess zu sehen.
- **Zeigen Sie Kantengehäusehandling** – z.B. wenn alle Batterien gleich sind, oder eine Batterie ist astronomische größer.
- **Mention Alternativen** – z.B. Prioritätswarte, DP – zum Nachweis der Wissensbreite, auch wenn Sie sich auf Sort-Trim für Kürze niederlassen.
- **Zeiten Sie Ihre Lösung** auf einem Whiteboard – stellen Sie sicher, dass Sie das veraltete 30-Minuten-Fenster nicht überschreiten.

### 9. Schlußfolgerung

LeetCode 2141 ist eine ordentliche Abbildung von **Grad-Trimm + arithmetische Argumentation*.
Indem Sie dieses Problem meistern, werden Sie ein starkes algorithmisches Denken, ein solides Verständnis von Ganzzahl-Arithmetik und die Fähigkeit, sowohl für *time* als auch *space* zu optimieren – genau die Qualifikationsrekrutierer suchen in Backend-, Data-Engineering- und Full-Stack-Rollen.

---

🔑 5️⃣ Warum dieser Blog hilft Ihnen, Ihren nächsten Job zu finden

- **Interview-ready*: Der Artikel geht durch die komplette Vernunft Pipeline.
- **Multi-Sprache*: Java, Python, C++ Schnipsel demonstrieren Cross-Plattform-Proficiency.
- **SEO‐freundlich**: Keywords wie *Maximale Laufzeit von N Computern*, *LeetCode 2141*, *binäre Suche*, *Kodierungsinterview*, *Java*, *Python*, *C++* sorgen für Sichtbarkeit bei Job-Suchmaschinen.
- **Clear-Struktur*: Rubriken, Tabellen und Code-Blöcke machen den Artikel einfach zu überspringen – ein großes Plus für Rekrutierer Scannen schnell.

---

### 📌 Takeaway

> **Sort‐and‐Trim** gibt Ihnen eine saubere, optimale Lösung, die in einem Interview leicht zu erklären ist.
> **Binary Search** bietet eine algorithmische Perspektive und beweist dasselbe Ergebnis mit einer anderen Linse.
> Was immer Sie präsentieren, bereit sein, Randfälle zu diskutieren und die Machbarkeitsprüfung zu rechtfertigen – das sind die „guten“ Interview-Momente, die einen dauerhaften Eindruck hinterlassen.

Viel Glück und glückliche Kodierung!