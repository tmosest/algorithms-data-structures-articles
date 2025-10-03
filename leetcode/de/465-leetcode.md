---
Titel: LeetCode 465. Optimaler Kontoausgleich - Ja.
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
oder 1. Code Solutions

Im Folgenden finden Sie **ready‐to‐run** Implementierungen für das LeetCode Hard Problem *Optimal Account Balancing* (Problem 465) in **Java 17*, **Python 3.11** und **C++17**.
Alle drei Versionen verwenden dieselbe Kernidee:
ANHANG Berechnen Sie die Nettobilanz jeder Person.
2. Halten Sie nur die Nicht-Null-Salden.
3. Verwenden Sie Backtracking + Memoization (bit-mask DP), um die minimale Anzahl von Siedlungen zu finden.

> ・️ *Tip*: Die rekursive DFS ist garantiert, in einigen Millisekunden für die gegebenen Zwänge zu beenden (`transactions.length ≤ 8`), so ist es perfekt für Interview-Praxis.

---

### Java 17

``java
Import java.util.*;

Public class Lösung {\cHFFFF}
public int minTransfers(int[][]transaktionen) {\cHFFFF}
// 1️⃣ Nettosalden aufbauen
Karte<Integer, Integer> bal = new HashMap<>;
für (int[] t : Transaktionen) {\cHFFFF}
Bal.merge(t[0], t[2], Integer::sum);
Bal.merge(t[1], -t[2], Integer::sum);
}

// 2️⃣ Nur die Nicht-Null-Salden halten
List<Integer> Schulden = new ArrayList<>>();
für (int v : bal.values())
(v != 0) Schulden.add(v);

int n = Schulden.size();
// 3️⃣ Memoization table: dp[mask] = minimale #settlements für diese Untermenge
int[] memo = neu int[1 << n;
Arrays.fill(memo, -1);
memo[0] = 0; // leerer Satz braucht 0 Transaktionen

Rückgabe n - dfs((1 << n) - 1, Schulden, Memo);
}

// DFS mit Memoization
Private Int dfs(int mask, List<Integer> Schulden, int[] memo) {
wenn (memo[mask] != -1) Rückkehr memo[mask];

Insgesamt Summe = 0, am besten = 0;
für (in i = 0; i < Schulden.size(); i++)
int bit = 1 << i;
wenn (mask & bit) != 0)
BalanceSum += Schulden.get(i);
best = Math.max(best, dfs(mask ^ bit, Schulden, memo));
}
}
// Wenn die Summe der Untermenge Null ist, können wir sie in 1 txn zusammensetzen
memo[mask] = best + (balanceSum == 0 ? 1 : 0);
zurück memo[mask];
}
}
`` `

---

### Python 3.11

```python
aus der Einfuhr Liste
von functools import lru_cache
aus Sammlungen Import Anzahl

Klasse Lösung:
def minTransfers(selbst, Transaktionen: List[List[int]]]) -> int:
# 1️⃣ Nettosaldo je Person erstellen
Ballen = Counter()
bei Transaktionen:
Ballen[frm] += am
Ballen[zu] -= am

# 2️⃣ Nur Nicht-Null-Salden halten
Schulden = [v für v in bal.values() wenn v]
n = len(Schulden)

@lru_cache(None)
def dfs(mask: int) -> int:
"""Return max. Anzahl von Null-Summe-Gruppen können wir aus Subset `mask`.""
wenn Maske == 0:
Rückkehr 0
Balance_sum = 0
= 0
für i im Bereich(n):
Bit = 1 < ≤ i
Wenn Maske & Bit:
balance_sum += Schulden[i]
best = max(best, dfs(mask ^ bit))
zurück am besten + (1 wenn balance_sum == 0 sonst 0)

# 3️⃣ Ergebnis: n - maximale #zero‐sum-Gruppen
Rückgabe n - dfs((1 << n) - 1)
`` `

---

C++17

```cpp
#include <bits/stdc++.h>
mit Namespace std;

Klasse Lösung {
öffentlich:
int minTransfers(vector<vector<int>>>&transaktionen) {\cHFFFF}
unordered_map<int, lang> bal;
für (auto &t : Transaktionen) {\cHFFFF}
Bal[t[0]] += t[2];
Bal[t[1]] -= t[2];
}

vektor<long long> Schulden;
für (Auto &p : Ballen)
wenn (Sek.) Schulden.push_back(Sek.)

int n = Schulden.size();
vektor<int> memo(1 << n, -1)
memo[0] = 0; // leerer Satz braucht 0 txns

Funktion<int(int)> dfs = [&](int mask) -> In den Warenkorb
wenn (memo[mask] != -1) Rückkehr memo[mask];
lange lange Summe = 0;
int best = 0;
für (in i = 0; i < n; ++i) {\cHFFFF}
wenn (Maske & (1 < ≤ i)
Summe += Schulden[i];
best = max(best, dfs(mask ^ (1 < ≤ i)));
}
}
memo[mask] = best + (sum = 0 ? 1 : 0);
zurück memo[mask];
};

Rückgabe n - dfs((1 << n - 1);
}
};
`` `

---

oder 2. Blog Artikel – „Optimales Kontobalancing: Das Gute, das Schlechte und das Böse“

> **SEO Keywords*: LeetCode 465, Optimal Account Balancing, hard algorithm, backtracking, DFS, bitmask DP, Interviewvorbereitung, Software-Ingenieur-Interview, Java-Lösung, Python-Lösung, C++-Lösung, Job-Interview-Tipps.

---

### Einführung

Wenn Sie LeetCode 465 – *Optimal Account Balancing* – Sie blicken auf ein klassisches **minimum‐transaction** Problem, das sich trügerisch einfach anfühlt, aber eigentlich ein **Hard** Problem ist. In einem realen Interview müssen Sie *Warum* einen Backtracking-Ansatz zu erklären, wie Sie den Suchraum stürzen, und warum die Lösung ist effizient genug für die Zwänge.

Unten gehen wir durch das **good*** (Warum ist das Problem ein tolles Interview-Thema), das **bad*** (was Fallstricke oft Kandidaten auslösen) und das **ugly*** (der naive Code, der Time-out wird). Wir werden mit einer polierten, produktionsfertigen Lösung in **Java**, **Python** und **C++** enden.

---

### The Good: Warum dieses Problem auftaucht

| Aspect | Warum es Nützlich ist |
|----------------------------
| **Graph of Debt** | Das Problem kann als gewichtetes Diagramm dargestellt werden. Es testet das Verständnis von *net flow*-Konzepten. |
| **Backtracking + Memoization** Demonstrate Mastery of Recursion, pruning und DP auf Subsets – Kernkompetenzen für jede ältere Rolle. |
| **Small Input, Exponential Search** | Zeigt, dass *time‐complexity* mehr als *space* zählt; der Interviewte muss die O(2^n) Natur erkennen und optimieren. |
| **Language‐agnostic** | Sie können es in Java, Python, C++, Rust lösen... die Logik bleibt das gleiche und beweist algorithmisches Denken über Sprachfluss. |
| **Job‐Search Edge** | Dieses Problem sauber zu lösen ist ein gemeinsamer Interview-Benchmark für fintech, fintech‐ähnliche Startups und jede datenschwere Rolle. Eine polierte Lösung wird auf Ihrem GitHub bemerkt. |

---

### The Bad: Common Pitfalls

| Pitfall | Warum es versagt |
|--------------------------
| **Treating Jede Person als Node** | Counting `from` und `to` separat kann zu 12 Knoten führen, aber die Anzahl der *effektiven* Personen ist ≤ 8. Vergessen, den Graph zu kollabieren, fügt nutzlose Arbeit. |
| **Not Pruning** | Eine naive DFS, die jedes Paar von Menschen in jedem Schritt erforscht `n!` Möglichkeiten – inakzeptabel für `n = 8`. |
| ** Verwenden von Karten für die Memoization** | Mit `Map<Integer, Integer>` mit einem *String-Schlüssel* für Subsets führt zu Hashing Overhead; ein Bitmask-Array ist schneller. |
| **Returning the Wrong Value** | Mixing up “minimal Transaktionen” vs “maximale Zero‐sum-Gruppen” – die richtige Antwort ist `n - maxZeroGroups`. |
| **Over‐Recursion** | Für große `n` kann die Recursionstiefe Javas Stacklimit oder Pythons Recursionslimit treffen. Ein schwanz-rekursiver oder iterativer Ansatz ist sicherer. |

---

### Die Ugly: Ein Naïve, Time‐Out Code

```python
# Ugly, O(n!) Python
def minTransfers(Transaktionen):
Salden = Zähler()
bei Transaktionen:
Salden[f] += am
Saldos[t] -= amt
Schulden = [v für v in balances.values() wenn v]
n = len(Schulden)
am besten = n
def dfs(i, cur):
nichtlokal am besten
wenn i == n:
best = min(best, cur)
zurück
dfs(i+1, cur+1) # versuchen, diese Person allein einzurichten
für j im Bereich (i+1, n):
wenn Schulden[i] + Schulden[j] == 0:
dfs(i+1, cur) # vereinbaren i mit j zusammen
dfs(0, 0)
zurück zur Übersicht
`` `

Dieser Code versucht jede mögliche Gruppierung von Menschen. Mit `n = 8` kann es **40320*** wiederkehrende Anrufe machen, und mit einem schweren Counter/Loop Overhead übertrifft es die 2 zweite Grenze auf LeetCode. Es ist *hässlich*, weil es sauber aussieht, aber in der Praxis scheitert.

---

### Die saubere, polierte Lösung

Alle drei folgenden Sprachen folgen der *same* optimalen Strategie:

ANHANG **Vernetzt die Waagen* (`from` + `amt`, `to` – `amt`).
2. **Keep nur Nicht-Null-Verschuldungen** – höchstens `n ≤ 8`.
3. **Bit‐mask DP** (`dp[mask]`) speichert die maximale Anzahl der Null-Summe-Gruppen, die wir für eine bestimmte Untermenge zusammenbrechen können.
4. Die endgültige Antwort lautet `n - dp[(1<n)-1] `.

oder Warum das funktioniert

*Jede Abwicklung, die die Summe einer Teilmenge auf **0** bringt, kann mit einer einzigen Transaktion gelöst werden. Durch *maximieren* die Anzahl solcher Nullsummengruppen minimieren wir die erforderlichen Transaktionen. *

Die Komplexität ist **O(2^n · n)** – für `n = 8`, das ist nur **512** gibt Zeiten einer winzigen inneren Schleife, die < 1 ms in Java und < 0,5 ms in Python auf moderner Hardware ist.

---

### Komplexitätsanalyse

| Sprache | Zeit | Raum |
|-------------------------
| **Java** | **O(2^n · n)** (`n ≤ 8`) | **O(2^n)* für Memo-Tabelle + `O(n)` Recursion Stack |
| **Python** | **O(2^n · n)** (gespeichert) | **O(2^n)** für LRU-Cache |
| **C++*** | **O(2^n · n** (array DP) | **O(2^n)** für Vektor <=

Da `n` bei 8 verdeckt ist, ist die Lösung praktisch *instant*.

---

### Fazit & Take-aways

* Optimale Account Balancing ist ein **must‐solve**-Problem für alle, die sich auf Data‐heavy oder Fintech-Rollen bewerben.
* Vermeiden Sie die häufigsten Fehler: Kollabieren Sie die Grafik, prune aggressiv, verwenden Sie bitmask memoization, und `n - maxZeroGroups` zurück.
* Die drei Code-Snippets oben sind **clean, testable und sprach-agnostisch** – perfekt für das Hinzufügen in Ihr Portfolio.

**Job-Search Tipp**: Legen Sie Ihre Java-, Python- und C++-Lösungen in einem einzigen Repo auf GitHub, markieren Sie sie `leetcode-465` und fügen Sie ein kleines README hinzu, das den Algorithmus erklärt. Recruiter lieben eine klare, gut ausgestattete Lösung.

Glückliche Kodierung – und können Ihre Interviewpartner immer oben herauskommen!