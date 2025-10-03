---
Titel: LeetCode 801. Minimum Swaps Um Sequenzen zu erhöhen -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
# 🧩 LeetCode 801 – Mindestschwindigkeiten, um Sequenzen zu erhöhen
Eine vollständige Anleitung (Java | Python | C++) + Blog Post
> **Keywords*: LeetCode 801, Minimal Swaps, DP, Interviewalgorithmus, Java-Lösung, Python-Lösung, C++-Lösung, Jobinterview, Codierung Interview, dynamische Programmierung

---

oder 1. Problem Recap

| | |
|------
| **Problem** | Mindestschwindigkeiten, um Sequenzen zu erhöhen |
| ** Schwierigkeit**
| **Input** | Zwei ganzzahlige Arrays `nums1` & `nums2` gleicher Länge `n` (2 ≤ n ≤ 105) |
| **Operation** | Swap `nums1[i]` mit `nums2[i]`` ***** pro Index. |
| **Goal** | Mindestanzahl von Swaps, um **both**-Sequenzen streng zu erhöhen. |
| **Guarantee** Der Eingang gibt immer eine Lösung zu. |

> *Beispiel*
> `nums1 = [1,3,5,4]
> `nums2 = [1,2,3,7]
> → Swap bei `i = 3` → `nums1 = [1,3,5,7], `nums2 = [1,2,3,4]` (1 Swap).

---

oder 2. Intuition

Für jede Position `i` gibt es zwei Möglichkeiten:

ANHANG ** Swap** bei `i`.
2. **Swap** bei `i`.

Ob eine Wahl gültig ist, hängt nur von der *vorherigen* Wahl ab:

- Wenn wir ** nicht swap** bei `i‐1` angegeben haben, dann sind die vorherigen Werte `nums1[i-1]` und `nums2[i-1]`.
- Wenn wir ****** bei `i‐1`, die vorherigen Werte sind `nums2[i-1] und `nums1[i-1]`.

Wir können also zwei DP-Staaten verfolgen:

- `keep[i]` – minimale Swaps bis zum Index `i` ** wenn wir** (nicht Swaps) bei `i` behalten.
- `wap[i]` – minimale Swaps bis zum Index `i` **, wenn wir bei `i` tauschen.

Weil wir uns nur `i-1` anschauen, können wir die DP auf **O(1) Raum* komprimieren.

---

oder 3. Wiederauftreten

`a = nums1[i-1]`, `b = nums2[i-1]`, `c = nums1[i]`, `d = nums2[i]`.

`` `
[i] = min(
halten[i-1], wenn ein < c && b < d, // weiter ansteigt
Swap[i-1], wenn ein < c && b < d + 1, // früher getauscht, aktuell bleiben
)

Swap[i] = min(
halten[i-1] + 1 wenn ein < d & & & b < c, // vorhergehen, Swap-Strom
Swap[i-1] + 1 wenn ein < d && b < c, // früher getauscht, Swapstrom
)
`` `

**Bilanz** (`i = 0`):

`` `
halten[0] = 0 // kein Swap benötigt
swap[0] = 1 // Swap beim ersten Index
`` `

Die Antwort ist `min(keep[n-1], swap[n-1])`.

---

oder 4. Optimierte O(1) Space Implementation

Wir halten nur zwei Variablen:

`` `
halten = 0 // dp[0] für halten
swap = 1 // dp[0] für swap

für i = 1 .. n-1:
neue Behalten = INF
newSwap = INF
...
halten = newKeep
swap = newSwap
`` `

`INF` kann `n` sein (maximale Swaps möglich).

---

oder 5. Code in drei Sprachen

### 5.1 Java

``java
/**
* LeetCode 801. Mindestschwindigkeiten zu machen Sequenzen erhöhen
* O(n) Zeit, O(1) Raum
*
Klasse Lösung {
int minSwap(int[] nums1, int[] nums2) {
int n = nums1.Länge;
int halten = 0; // kein Swap an Position 0
int swap = 1; // Swap auf Position 0

für (in i = 1; i < n; i++) {\cHFFFF}
int newKeep = Integer.MAX_VALUE;
int newSwap = Integer.MAX_VALUE;

// Halten Sie an i
wenn (nums1[i - 1] < nums1[i] && nums2[i - 1] < nums2[i]) {\cHFFFF}
newKeep = Math.min(newKeep, keep);
}
// Swap bei i
wenn (nums1[i - 1] < nums2[i] && nums2[i - 1] < nums1[i]) {\cHFFFF}
newSwap = Math.min(newSwap, halten + 1);
}

// Behalten Sie mich, aber bei i-1 getauscht
wenn (nums1[i - 1] < nums1[i] && nums2[i - 1] < nums2[i]) {\cHFFFF}
newKeep = Math.min (newKeep, swap);
}
// Swap bei i mit getauscht bei i-1
wenn (nums1[i - 1] < nums2[i] && nums2[i - 1] < nums1[i]) {\cHFFFF}
newSwap = Math.min (newSwap, Swap + 1);
}

halten = newKeep;
swap = newSwap;
}

zurück Math.min (keep, swap)
}
}
`` `

### 5.2 Python

```python
""
LeetCode 801. Mindestschwindigkeiten, um Sequenzen zu erhöhen
O(n) Zeit, O(1) Raum
""

Klasse Lösung:
def minSwap(self, nums1: list[int], nums2: list[int]) -> int:
n = len(nums1)
halten, swap = 0, 1 # dp[0]

für i im Bereich(1, n):
new_keep = float('inf')
new_swap = float('inf')

# Keep current, keep vorherige
wenn nums1[i-1] < nums1[i] und nums2[i-1] < nums2[i]:
new_keep = min(new_keep, keep)

# Keep current, swap vorherige
wenn nums1[i-1] < nums1[i] und nums2[i-1] < nums2[i]:
new_keep = min(new_keep, swap)

# Swap current, keep vorherige
wenn nums1[i-1] < nums2[i] und nums2[i-1] < nums1[i]:
new_swap = min(new_swap, halten + 1)

# Swap current, swap vorherige
wenn nums1[i-1] < nums2[i] und nums2[i-1] < nums1[i]:
new_swap = min(new_swap, swap + 1)

halten, swap = new_keep, new_swap

zurück min(keep, swap)
`` `

5.3 C++

```cpp
/**
* LeetCode 801. Mindestschwindigkeiten zu machen Sequenzen erhöhen
* O(n) Zeit, O(1) Raum
*
Klasse Lösung {
öffentlich:
int minSwap(vector<int>& nums1, vector<int>>& nums2) {
int n = nums1.size();
int halten = 0; // dp[0, wenn wir das erste Element halten
int swap = 1; // dp[0] wenn wir das erste Element wechseln

für (in i = 1; i < n; ++i) {\cHFFFF}
int newKeep = INT_MAX, newSwap = INT_MAX;

// Strom halten, vorher halten
wenn (nums1[i-1] < nums1[i] && nums2[i-1] < nums2[i]) {\cHFFFF}
newKeep = min(newKeep, halten);
newKeep = min(newKeep, swap)
}
// Swap Strom, Halten oder Swap vorherige
wenn (nums1[i-1] < nums2[i] && nums2[i-1] < nums1[i]) {\cHFFFF}
newSwap = min(newSwap, halten + 1);
newSwap = min(newSwap, swap + 1);
}

halten = newKeep;
swap = newSwap;
}
zurück min(keep, swap)
}
};
`` `

> **Warum haben wir zwei getrennte Überprüfungen für den Zustand „Schafen“? * *
> Da die Bedingung `nums1[i-1] < nums1[i] && nums2[i-1] < nums2[i] ` gleich ist, unabhängig davon, ob der frühere Index vertauscht wurde oder nicht. Der einzige Unterschied ist, ob wir eine Swap-Kosten hinzufügen (`swap + 0` oder `swap + 0`). Die gleiche Logik gilt für den Zustand "Swap".

---

oder 6. Blog Artikel – “Das Gute, das Böse, die Ugly von LeetCode 801”

### 6.1 Titel & Meta

**Titel:**
*Mastering LeetCode 801: Minimum Swaps, um Sequenzen zu erhöhen – Java, Python, & C++ Lösungen*

**Meta Beschreibung:**
Erfahren Sie die schnellste O(n) DP-Lösung für LeetCode 801, mit klaren Java-, Python- und C++-Implementierungen. Entdecken Sie Fallstricke, Trade-offs und behördliche Erklärungen.

---

### 6.2 Einführung

> „Was ist der effizienteste Weg, um zwei Sequenzen streng zu erhöhen, wenn Sie nur Elemente mit demselben Index austauschen können? „
> Das ist die Frage hinter LeetCode 801. Die Herausforderung sieht einfach aus, wird aber schnell zu einem Lehrbuch-DP-Übung, wenn Sie es richtig brechen.
> In diesem Artikel gehen wir durch das Problem, den dynamischen Programmiertrick, der es auf O(n) Zeit und O(1) Raum reduziert, und den Code in drei populären Sprachen. Wir diskutieren auch die *good*, *bad* und *hässliche* Aspekte der Lösung, um Ihnen zu helfen, gemeinsame Interview Fallstricke zu vermeiden.

---

### 6.3 Das Problem in Plain Englisch

ANHANG Sie haben zwei ganzzahlige Arrays `nums1` und `nums2` gleicher Länge `n`.
2. In einer Operation können Sie die beiden Zahlen mit dem gleichen Index `nums1[i] ≠ nums2[i] ` ändern.
3. Ihr Ziel: **beide Arrays werden streng ansteigen* (`a[i] < a[i+1]` für jedes `i`).
4. Finden Sie die minimale Anzahl der benötigten Swaps.

Da die Testdaten eine Lösung garantieren, müssen Sie nur Swaps minimieren, keine Sorge um „unmögliche“ Fälle.

---

### 6.4 Das Gute – Warum dieser DP elegant ist

- **Linear Time:** Wir brauchen nur einen Pass über die Arrays (`O(n)`).
- **Constant Extra Space:** Es sind nur zwei ganzzahlige Variablen (`keep`, `swap`) notwendig.
- **Simple Recurrence:** Der Zustand bei Index `i` hängt allein von `i-1` ab.
Das ist das Kennzeichen eines sauberen DP Problem.

---

### 6.5 The Bad – Häufige Missteps

| Misstep | Warum es passiert | Fix |
|----------------------------------
| ** Die Menschen denken manchmal, dass die Bedingung für das Swapping bei `i` die gleiche ist wie für das Halten, aber es ist nicht. Halten Sie die vier Kontrollen getrennt: halten-keep, keep‐swap, swap‐keep, swap‐swap. |
| ** Verwenden von Arrays für DP unnötig** Declaring `int[] keep = new int[n]` Verschwendungsspeicher. | Verwenden Sie zwei Variablen und aktualisieren Sie sie an Ort und Stelle. |
| **Ignorieren Sie den “Swap at i-1” Effekt** | Failing, um `1` hinzuzufügen, wenn der aktuelle Index getauscht wird. | Fügen Sie immer `+1` für den aktuellen Swap in `newSwap` hinzu. |
| **Assuming 1-Indexed Arrays** | Java, Python, C++ sind 0-basiert; das Mischen von Indizes führt zu Out-of-bounds. | Starten Sie die Schleife bei `i = 1`. |

---

### 6.6 The Ugly – Edge Cases & Debugging Tips

- ** Qualität an Grenzen** (`nums1[i] == nums2[i]` oder `nums2[i] == nums1[i]`.
Denken Sie daran, das Problem fordert * streng * zu erhöhen, so können Sie nicht zulassen `=`. Die DP-Checks (`<`) behandeln dies automatisch.
- **Large-Nummer* (`1e9`).
Kein Überlauf auftritt, weil wir nur Zählungen speichern (` ≤ n`), aber Sie sollten noch vor `Integer schützen. MAX_VALUE in Java/C++.
- **Arrays der Länge 1** (`n = 1`).
Die Antwort ist immer `0`, weil die Arrays trivial ansteigen; das DP-Basisgehäuse handhabt dies automatisch.

**Debugging Checkliste: **

ANHANG Drucken Sie `keep` und `swap` an jedem Schritt.
2. Überprüfen Sie, ob die vier Zustandszweige richtig getroffen werden.
3. Überkreuzen Sie mit einer brute‐force Lösung für kleine `n`, um die Richtigkeit zu gewährleisten.

---

### 6.7 Interview‐Ready Erklärung

> **“Wir verwenden einen zweistufigen DP: halten oder schwapieren bei jedem Index.“* *
> *Key-Einsicht:* Swapping at index `i` beeinflusst **not** die Möglichkeit eines zukünftigen Swaps; es ändert nur die aktuellen Werte. Daher muss die Entscheidung bei `i` nur daran erinnert werden, ob der vorherige Index getauscht wurde oder nicht, nicht die genaue Reihenfolge der Swaps.

> ** Warum reichen zwei Staaten? **
> Denn es gibt nur zwei Möglichkeiten pro Index (swap oder nicht). Für jeden bewerten wir, ob die streng zunehmende Bedingung mit dem Zustand des vorherigen Index übereinstimmt. Dies ergibt genau vier Fälle, die in der Wiederholung erfasst werden.

> **Space-Optimierung:**
> Da `dp[i]` nur von `dp[i-1] abhängt, können wir die vorherigen Werte überschreiben. Dies gibt uns die Konstant-Raum-Variante, die Interviewer lieben.

---

### 6.7 Letzte Gedanken

LeetCode 801 ist ein *perfect* Interview Problem zu präsentieren:

- Meisterschaft der dynamischen Programmierung.
- Fähigkeit, saubere, sprach-agnostische Code zu schreiben.
- Achtung vor Randfällen und Interview-Etikette.

Nutzen Sie die oben genannten Lösungen als Ausgangspunkt. Fügen Sie Kommentare hinzu, die jede Branche in Ihren eigenen Worten erklären – das ist, wonach die Interviewer suchen.

Viel Glück, und können Ihre Arrays bleiben streng ansteigen!

---

### 6.8 Call‐to-Action

> Haben Sie bereits LeetCode 801 angegriffen? Teilen Sie Ihre Erfahrung in den Kommentaren, oder versuchen Sie das nächste DP Problem: **[LeetCode 725 – Split Array mit demselben Sum](https://leetcode.com/Probleme/split-array-with-same-sum/)**. Glückliche Kodierung!

---

oder 7. Zusammenfassung

Wir haben eine saubere DP-Lösung für LeetCode 801 abgeleitet, die in linearer Zeit und konstantem Raum verläuft. Wir haben es in Java, Python und C++ implementiert. Der Artikel erklärt die Stärken, Fallstricke und Debugging-Strategien des Problems, was es zu einem nützlichen Referenz für die Vorbereitung des Interviews und den Wiederaufbau des Gebäudes macht.