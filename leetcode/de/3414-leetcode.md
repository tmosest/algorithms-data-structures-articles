---
Titel: LeetCode 3414. Maximale Zugabe von nicht überschneidenden Intervallen -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
---

oder 1. Das Problem in einer Muschel

Wir haben **N ≤ 50 000** Intervalle

`` `
[li , ri , wi] (1 ≤ li ≤ ri ≤ 109, 1 ≤ wi ≤ 109)
`` `

und wir müssen wählen **bei den meisten vier* von ihnen, so dass

* keine zwei gewählten Intervalle berühren sich (das rechte Ende eines muss * begrenzt* kleiner sein als das linke Ende des anderen),
* das Gesamtgewicht maximal ist, und
* wenn mehrere Teilmengen das gleiche Maximalgewicht geben, geben wir die **lexicographisch kleinste Liste der ursprünglichen Indizes** zurück (Indizes sind 0-basiert in der Reihenfolge, in der die Intervalle in der Eingabe erscheinen).

Die benötigte Ausgabe ist die Liste der ursprünglichen Indizes in zunehmender Reihenfolge – das ist die Liste, die durch einfache Sortierung der Indizes erhalten würde.

> *Warum “bei den meisten vier” Angelegenheiten* – denn wir können uns einen vollen dynamischen Programmiertisch mit einer zusätzlichen Dimension leisten **k ε {0,...,4}**.
> *Warum die Grenzregel zählt* – die Aufteilung eines linken oder rechten Endpunktes gilt als überlappend, daher ist die *strict* Bedingung `ri < lj` (oder umgekehrt) diejenige, die halten muss.

Hier finden Sie drei Referenzlösungen, eine in **Python*, eine in **Java** und eine in **C++**. Alle drei lösen das Problem in **O(N log N)** Zeit und **O(N)** Speicher – bequem innerhalb der Grenzen.

---

oder 2. Der Algorithmus (gleiche Idee in allen drei Sprachen)

ANHANG **Indizes speichern**
Speichern Sie das 4‐tuple `(l, r, w, idx)` für jedes Intervall, wo `idx` die Position im Eingang (0-basiert) ist.

2. **Sort am linken Endpunkt*
Dies gibt uns eine deterministische Ordnung, in der wir die Intervalle erkunden werden.

3. **Pre-computing ‚next‘ Indizes**
Für jedes Intervall `i` benötigen wir das erste Intervall, das *nach* `ri` beginnt.
Da die Berührung des Endpunktes verboten ist, suchen wir nach dem kleinsten `j > i` mit
`lj > ri`.
Der Binär-Suchschritt verwendet die sortierte Liste der linken Enden.

4. ** Dynamische Programmierung mit einer zusätzlichen Dimension `k`**
`dp[i][k]` = best (Gewicht, Liste der ausgewählten Indizes) erreichbar ab Intervall `i`, wenn wir maximal `k` mehr Intervalle (`k` ε {0,1,2,3,4}) nehmen dürfen.
Die Wiederholung ist die klassische Wahl „take / skip“:

* **Skip** `i` → `dp[i+1][k] `
**take*** `i` → `wi + dp[next[i][k-1] ` und `idxi` in die Indizesliste einfügen

Da die Liste immer sortiert ist und höchstens 4 Zahlen enthält, ist das Zusammenführen / Sortieren der neuen Liste trivial.

5. **Tie-breaking*
Wenn die beiden Entscheidungen das gleiche Gesamtgewicht geben, müssen wir die *lexicographisch kleinste* Indexliste zurückgeben.
Lexikographischer Vergleich von zwei sortierten Indexlisten ist einfach Element-by-Element-Vergleich (z.B. Tupel-Vergleich in Python oder `std::lexicographical_compare` in C++).

6. **Antwort**
Starten Sie die Rekursion (oder die untenstehende DP) von `i = 0` und `k = 4`.
Die daraus resultierende Indizesliste ist die erforderliche Antwort.

---

oder 3. Referenzumsetzungen

### 3.1 Python 3

```python
#/usr/bin/env python3
Import sys
Bisect importieren
von functools import lru_cache
aus der Einfuhr Liste, Tuple

def max_weight_intervals(intervals: List[List[int]]]) -> Liste[int]:
""
Gibt die lexikographisch kleinste Liste der Originalindizes zurück
die das maximale Gewicht mit maximal 4 nicht überschneidenden Intervallen gibt.
""
n = len(Intervalle)
# Original Indizes anhängen und nach links sortieren
Artikel = [(l, r, w, idx) für idx, (l, r, w) in enumerate(Intervals)]
Artikelsort(key=lambda x: x[0])

beginnt = [x[0] für x in Items
nxt = [bisect.bisect_right(starts, Items[i][1]) für i in range(n)]

@lru_cache(maxsize=None)
def dfs(i: int, k: int) -> Tuple[int, Tuple[int, ...]]:
"""Return (Score, tuple_of_indices) aus Position i mit höchstens k Picks.""
wenn k ==0 oder i == n:
zurück 0, ()
# skip
Skip_score, skip_list = dfs(i + 1, k)

♪ Take
Take_score, take_list = dfs(nxt[i], k - 1)
: Artikel[i][2]
new_list = tuple(sortiert(take_list + (items[i][3],)))

# best
wenn Take_score > - Was?
zurück Take_score, new_list
wenn Take_score < skip_score
zurück skip_score, skip_list
# gleichgewicht → lexicographicvergleich
zurück take_score, min(skip_list, new_list)

best_score, best_indices = dfs(0, 4)
Rückgabeliste(best_indices)


...
wenn __name__== "__main__":
Daten = sys.stdin.read().strip().splitlines()
wenn nicht Daten:
sys.exit(
N = int(Daten[0])
Intervalle = [list(map(int, line.split()))) für Zeile in Daten[1:N + 1]]
res = max_weight_intervals(intervals)
print(" ".join(map(str, res)))
`` `

** Erklärung**

* `@lru_cache` garantiert, dass jedes `(i, k)` Paar nur einmal berechnet wird.
* Die Rekursionstiefe wird durch `N` begrenzt, aber das Caching verhindert ein Aufblasen: nur ~N × 5 Zustände existieren.
* `tuple(sorted(...)` garantiert, dass die Liste sortiert und für den lexicographic Vergleich bereit ist.

---

### 3.2 Java 17

``java
Einfuhr java.io.*;
Import java.util.*;

Volksklasse Main {\cHFFFF}

Private statische Klasse Interval {
int l, r, w, idx;
Interval(int l, int r, int w, int idx) {\cHFFFF}
Diese.l = l; this.r = r; this.w = w; this.idx = idx;
}
}

private statische Klasse Ergebnis {
lange Punktzahl;
List<Integer> Indizes; // sortiert
Ergebnis(Langergebnis, List<Integer> Indizes) {
das. Score = Score;
Diese.Indizes = Indizes;
}
}

Public statische List<Integer>solv(List<int[]> roh)
int n = roh.size();
List<Interval> Items = new ArrayList<>(n);
für (in i = 0; i < n; i++) {
int[] a = roher.get(i);
Items.add(new Interval(a[0], a[1], a[2], i));
}
items.sort(Comparator.comparingInt(o -> o.l));

int[] beginnt = neu int[n];
für (in i = 0; i < n; i++) beginnt[i] = Items.get(i).l;
int[] next = new int[n];
für (in i = 0; i < n; i++) {
int pos = topBound(starts, items.get(i).r);
nächstes[i] = pos;
}

Long[][] bestScore = new long[n + 1][5];
@SuppressWarnings("unchecked")
Liste<Integer>[][ bestList = neue Liste[n + 1][5];
für (in k = 0; k <= 4; k++) {
bestScore[n][k] = 0;
bestList[n][k] = Collections.emptyList();
}

für (in i = n - 1; i >= 0; i-)
für (in k = 0; k <= 4; k++) {
Long skipScore = bestScore[i + 1][k];
Liste<Inger> SkipList = bestList[i + 1][k];

wenn (k == 0) { // nichts mehr zu wählen
bestScore[i][k] = skipScore;
bestList[i][k] = skipList;
weiter;
}

int ni = next[i];
lange Ergebnis = Items.get(i).w + bestScore[ni][k - 1];
List<Integer> takeList = new ArrayList<>(bestList[ni][k - 1]);
TakeList.add(items.get(i).idx);
Sammlungen.sort(takeList);

wenn (takeScore > skipScore)
bestScore[i][k] = nehmen Partitur
bestList[i][k] = nehmen Liste
} auch wenn (takeScore < skipScore)
bestScore[i][k] = skipScore;
bestList[i][k] = skipList;
} sonst { // gleichgewicht – lexicographic tie‐break
bestScore[i][k] = nehmen Partitur
bestList[i][k] = lexicographicMin(SkipList, TakeList),
}
}
}
Rückkehr bestList[0][4];
}

// gibt die lexikographisch kleinere von zwei sortierten Listen zurück
Private statische List<Integer> lexicographicMin(List<Integer> a, List<Integer> b) {
int i = 0;
(i < a.size() && i < b.size() {\cHFFFF}
int va = a.get(i), vb = b.get(i);
wenn (va != vb) va < vb zurückgegeben werden?
i++;
}
a.size() <= b.size()
}

// obere Begrenzung auf einem sortierten Array
Private statische Int obereBound(int[] arr, int key) {
int l = 0, r = arr.length;
(l < r)
int m = (l + r) >> 1;
wenn (arr[m] <= key) l = m + 1;
n = m;
}
Rückgabe l;
}

// -------- Haupt --------
öffentlicher statischer Leerlauf (String[] args) wirft IOException {
BufferedReader br = neuer BufferedReader (neuer InputStreamReader(System.in));
int n = Integer.parseInt(br.readLine().trim());
Liste<int[]> ro = new ArrayList<>>();
für (in i = 0; i < n; i++) {
String[] Teile = br.readLine().trim().split("\s+");
ro.add(neue Int[]{Integer.parseInt(parts[0]),
Integer.parseInt(Teile[1]),
Integer.parseInt(Teile[2])});
}
List<Integer> ans =solv(raw)
StringBuilder sb = neuer StringBuilder();
für (in i = 0; i < ans.size(); i++)
wenn (i > 0) sb.append(');
sb.append(ans.get(i));
}
System.out.println(sb);
}
}
`` `

**Key Points* *

* `@lru_cache` garantiert O(1) pro Staat.
* `min(SkipList, newList)` verwendet einen Tupel-Vergleich – der lexikographisch kleinere Tupel wird automatisch gewählt, wenn die Gesamtgewichte gleich sind.

---

### 3.3 Java 17 (unt‐up DP – keine Wiederholung)

``java
Einfuhr java.io.*;
Import java.util.*;

Volksklasse Main {\cHFFFF}
Private statische Klasse Interval {
int l, r, w, idx;
Interval(int l, int r, int w, int idx) {\cHFFFF}
Diese.l = l; this.r = r; this.w = w; this.idx = idx;
}
}

Private statische List<Integer> Lösegeld (List<int[]> roh)
int n = roh.size();
List<Interval> Items = new ArrayList<>(n);
für (in i = 0; i < n; i++) {
int[] a = roher.get(i);
Items.add(new Interval(a[0], a[1], a[2], i));
}
items.sort(Comparator.comparingInt(o -> o.l));

int[] beginnt = neu int[n];
für (in i = 0; i < n; i++) beginnt[i] = Items.get(i).l;
int[] next = new int[n];
für (in i = 0; i < n; i++) {
next[i] = topBound(starts, items.get(i).r);
}

Long[][] bestScore = new long[n + 1][5];
@SuppressWarnings("unchecked")
Liste<Integer>[][ bestList = neue Liste[n + 1][5];
für (in k = 0; k <= 4; k++) {
bestScore[n][k] = 0;
bestList[n][k] = Collections.emptyList();
}

für (in i = n - 1; i >= 0; i-)
für (in k = 0; k <= 4; k++) {
// Schikanen
Long skipScore = bestScore[i + 1][k];
Liste<Inger> SkipList = bestList[i + 1][k];

wenn (k == 0) { // nichts anderes zu nehmen
bestScore[i][k] = skipScore;
bestList[i][k] = skipList;
weiter;
}

// nehmen
int ni = next[i];
lange Ergebnis = Items.get(i).w + bestScore[ni][k - 1];
List<Integer> takeList = new ArrayList<>(bestList[ni][k - 1]);
TakeList.add(items.get(i).idx);
Sammlungen.sort(takeList);

wenn (takeScore > skipScore)
bestScore[i][k] = nehmen Partitur
bestList[i][k] = nehmen Liste
} auch wenn (takeScore < skipScore)
bestScore[i][k] = skipScore;
bestList[i][k] = skipList;
} sonst { // gleichgewicht – lexicographic min
bestScore[i][k] = nehmen Partitur
bestList[i][k] = lexicographicMin(SkipList, TakeList),
}
}
}
Rückkehr bestList[0][4];
}

// obere Begrenzung auf sortierten linken Endpunkten
Private statische Int obereBound(int[] arr, int key) {
int l = 0, r = arr.length;
(l < r)
int m = (l + r) >> 1;
wenn (arr[m] <= key) l = m + 1;
n = m;
}
Rückgabe l;
}

// gibt die lexikographisch kleinere von zwei sortierten Listen zurück
Private statische List<Integer> lexicographicMin(List<Integer> a, List<Integer> b) {
int i = 0;
(i < a.size() && i < b.size() {\cHFFFF}
int va = a.get(i), vb = b.get(i);
wenn (va != vb) va < vb zurückgegeben werden?
i++;
}
a.size() <= b.size()
}

öffentlicher statischer Leerlauf (String[] args) wirft IOException {
BufferedReader br = neuer BufferedReader (neuer InputStreamReader(System.in));
int n = Integer.parseInt(br.readLine().trim());
Liste<int[]> ro = new ArrayList<>>(n)
für (in i = 0; i < n; i++) {
String[] Teile = br.readLine().trim().split("\s+");
ro.add(neue Int[]{Integer.parseInt(parts[0]),
Integer.parseInt(Teile[1]),
Integer.parseInt(Teile[2])});
}
List<Integer> ans =solv(raw)
StringBuilder sb = neuer StringBuilder();
für (in i = 0; i < ans.size(); i++)
wenn (i > 0) sb.append(');
sb.append(ans.get(i));
}
System.out.println(sb);
}
}
`` `

**Warum unten? **

* Recursion mit Memoization könnte auch funktionieren, aber eine einfache iterative DP eliminiert jedes Risiko von Stack-Überlauf und ist sehr einfach zu verstehen.

---

### 3.4 Python 3 (alternative Kurzform)

```python
defsolv():
Import sys
Daten = sys.stdin.read().strip().split()
wenn nicht Daten:
zurück
es = iter(data)
n = int(next(it))
roh = [(int(next(it)), int(next(it)), int(next(it)))) für _ in range(n)]
ro.sort(key=lambda x: x[0]) # Sortieren nach links Endpunkt

beginnt = [x[0] für x in Rohform
def top_bound(a, key):
l, r = 0, len(a)
während l < r:
m = (l + r) >> 1
wenn a[m] <= Schlüssel: l = m + 1
andere: r = m
zurück

next_idx = [upper_bound(starts, x[1]) für x in Rohform]
dp_score = [[0]*5 für _ im Bereich(n+1)]
dp_list = [[[]]*5 für _ in range(n+1)]
für i im Bereich (n-1, -1, -1):
für k im Bereich(5):
Skip_score = dp_score[i+1][k]
SPS_list = dp_list[i+1][k]
wenn k==0:
dp_score[i][k] = skip_score
dp_list[i][k] = skip_list
weiter
Take_score = Roh[i][2] + dp_score[next_idx[i]][k-1]
Take_list = sortiert(dp_list[next_idx[i][k-1] + [i])
wenn Take_score > - Was?
dp_score[i][k] = take_score; dp_list[i][k] = take_list
elif take_score < skip_score:
dp_score[i][k] = skip_score; dp_list[i][k] = skip_list
andere: # gleiches Gewicht
dp_score[i][k] = Take_score
dp_list[i][k] = min(skip_list, take_list)
Druck(' '.join(map(str, dp_list[0][4])))
`` `

---

### 3.5 C++ 17

```cpp
#include <bits/stdc++.h>
mit Namespace std;

struct Interval {\cHFFFF}
int l, r, w, idx;
};

Int highBound(const vector<int>& a, int key) {\cHFFFF}
int l = 0, r = (int)a.size();
(l < r)
int m = (l + r) >> 1;
wenn (a[m] <= Schlüssel) l = m + 1;
n = m;
}
Rückgabe l;
}

int main() {\cHFFFF}
ios::sync_with_stdio(false);
cin.tie(nullptr);
int n;
wenn (!(cin >> n)) 0 zurückgegeben wird;
Vektor<Interval> v;
für (in i = 0; i < n; ++i) {\cHFFFF}
> > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > >
v.emplace_back(l, r, w, i),
}
Art(v.begin(), v.end(), [](const Interval& a, const Interval& b){ return a.l < b.l); };

Vektor<int> startet(n)
für (in i = 0; i < n; ++i) beginnt[i] = v[i].l;
Vektor<int> nxt(n)
für (int i = 0; i < n; ++i) nxt[i] = obererBound(starts, v[i].r);

vektor<array<long long,5>> score(n+1);
vektor<array<vector<int>>> lst(n+1)
für (int k = 0; k <= 4; ++k) {
= 0;
lst[n][k] = {};
}

für (in i = n-1; i >= --i)
für (int k = 0; k <= 4; ++k) {
Langschürze = Score[i+1][k];
constvektor<int>& skipL = lst[i+1][k];

(k == 0)
Score[i][k] = SPS;
lst[i][k] = SPS
weiter;
}

lange TakeS = v[i].w + Score[nxt[i]][k-1];
Vektor<int> TakeL = lst[nxt[i][k-1];
TakeL.push_back(v[i].idx);
sort(takeL.begin(), takeL.end());

wenn (takes > skipS)
Score[i][k] = TakeS;
lst[i][k] = TakeL;
} auch wenn
Score[i][k] = SPS;
lst[i][k] = SPS
} auch
// gleich – lexicographic min
Score[i][k] = TakeS;
// lexicographic min von zwei sortierten Vektoren
const vector<int>& a = skipL, &b = takeL;
Vektor<int> res = a;
bool weniger = falsch;
für (size_t t = 0; t < min(a.size(), b.size()); ++t)
wenn (a[t] != b[t]) {\cHFFFF}
weniger = a[t] < b[t];
Bruch;
}
}
wenn (weniger) res = a;
wenn (a.size() > b.size() res = b;
lst[i][k] = res;
}
}
}
für (size_t i = 0; i < lst[0][4].size(); ++i)
wenn (i) cout << '';
cout << lst[0][4][i];
}
cout << '\n';
}
`` `

**Highlights* *

* verwendet `vector<array>>>> für DP-Arrays (feste Größe 5 für `k`).
* Der Lexikographische Vergleich erfolgt manuell mit einer kleinen Schleife.

---

### 3.6 C# 11

```csharp
mit System;
mit System. Sammlungen. Generisch;
mit System. IO;
mit System. Linq;

Programm der Öffentlichkeit
{\cHFFFF}
Privatrekord Interval(int L, int R, int W, int Id);

Privatrekord Ergebnis(langer Punkt, List<int> Indices);

öffentliche statische Leerstelle Main()
{\cHFFFF}
var input = Console.ReadLine();
wenn (Eingang = = Null) zurückkehrt;
int n = int.Parse(Eingang);
var ro = new List<int[]>();
für (in i = 0; i < n; i++)
{\cHFFFF}
var Teile = Konsole.ReadLine().Split(', StringSplitOptionen.RemoveEmptyEntries);
roh. Int.Parse(parts[0]), int.Parse(parts[1]), int.Parse(parts[2]) });
}

var ans = Solve(Roh)
Console.WriteLine(string.Join(', ans));
}

Private statische List<int> Solve(List<int[]> Roh
{\cHFFFF}
int n = roh. Anzahl
var Items = new List<Interval>(n);
für (in i = 0; i < n; i++)
Artikel. Hinzufügen (neue Intervall(raw[i][0], roh[i][1], roh[i][2], i));

Artikel.Sort((a, b) => a.L.CompareTo(b.L));

int[] beginnt = Items.Select(x => x.L).ToArray();
int[] next = new int[n];
für (in i = 0; i < n; i++)
nächstes[i] = UpperBound(Start, Items[i].R);

Long[][] bestScore = new long[n + 1][];
Liste<int>[[][] bestList = new List<int>[n + 1][];
für (in k = 0; k <= 4; k++)
{\cHFFFF}
bestScore[n] = new long[5];
bestList[n] = new List<int>[5];
für (int kk = 0; kk <= 4; kk++)
{\cHFFFF}
bestScore[n][kk] = 0;
bestList[n][kk] = new List<int>();
}
}

für (in i = n - 1; i >= 0; i-)
{\cHFFFF}
für (in k = 0; k <= 4; k++)
{\cHFFFF}
Long skipScore = bestScore[i + 1][k];
Liste<int> skipList = bestList[i + 1][k];

(k == 0)
{\cHFFFF}
bestScore[i][k] = skipScore;
bestList[i][k] = skipList;
weiter;
}

lange Ergebnis = Elemente[i]. W + bestScore[next[i][k - 1];
var takeList = new List<int>(bestList[next[i]][k - 1]) { Items[i]. Id.
TakeList.Sort();

wenn (takeScore > skipScore)
{\cHFFFF}
bestScore[i][k] = nehmen Partitur
bestList[i][k] = nehmen Liste
}
(takeScore < skipScore)
{\cHFFFF}
bestScore[i][k] = skipScore;
bestList[i][k] = skipList;
}
andere // gleiches Gewicht
{\cHFFFF}
bestScore[i][k] = nehmen Partitur
// lexicographic min
bestList[i][k] = LexicographicMin(SkipList, TakeList),
}
}
}
Rückkehr bestList[0][4];
}

Private statische Int UpperBound(int[] a, Int key)
{\cHFFFF}
int l = 0, r = a.Length;
(l < r)
{\cHFFFF}
int m = (l + r) / 2;
wenn (a[m] <= Schlüssel) l = m + 1;
n = m;
}
Rückgabe l;
}

Private statische List<int> LexicographicMin(List<int> a, List<int> b)
{\cHFFFF}
int len = Math.Min(a.Count, b.Count);
für (in i = 0; i < len; i++)
{\cHFFFF}
wenn (a[i] != b[i]) ein[i] < b[i] ? a: b[i] zurückgibt;
}
zurück a.Count <= b.Count? a: b;
}
}
`` `

* C# 11 verwendet `record` für Kürze und unveränderliche Datenstrukturen.

---

oder 4. Erklärung des Algorithmus (Dynamic Programming)

ANHANG **Sortung**
Alle Intervalle werden nach dem linken Endpunkt \(L_i\) sortiert.
Dies garantiert, dass, wenn das Intervall *j* später beginnt als *i* (\(L_j > L_i\)), dann in der sortierten Reihenfolge *j* nach *i* erscheint.
Die für die DP-Rekursion benötigte Eigenschaft ist:
*Das rechte Intervall, das vor dem linken Endpunkt des aktuellen Intervalls endet, ist der Vorgänger. *
Da die Intervalle nach *L* sortiert werden, kann dieser Vorgänger mit einer binären Suche auf dem Array der linken Endpunkte gefunden werden.

2. ** Dynamische Programmierung**
Für jede Position *i* (Interval *i*) und für jede Anzahl *k* der bereits ausgewählten Intervalle (\(0\le k\le 4\) speichern wir:
* `dp_score[i][k]` – Maximales Gesamtgewicht, das unter Berücksichtigung nur der Intervalle mit Indizes ≥ i erreichbar ist, wenn *k* Intervalle bereits gewählt wurden.
* `dp_list[i][k]` – die entsprechende sortierte Indizesliste.

Recurrence for Intervall *i* (0-based index):

`` `
skip: Wählen Sie nichts aus Intervall i
Ergebnis = dp_score[i+1][k]
Liste = dp_list[i+1][k]

nehmen: wählen Sie Intervall i (muss sich nicht mit einem später gewählten Intervall überschneiden)
p = next_index[i] // erstes Intervall beginnend nach R_i
Punkt = Gewicht[i] + dp_score[p][k-1]
Liste = sortiert( dp_list[p][k-1] ∪ {i} )
`` `

Wenn sich die beiden Punkte unterscheiden, behalten wir die größere.
Wenn die Punkte gleich sind, halten wir die *lexicographisch kleinste* Indexliste – dies ist das, was die Aussage verlangt.

3. **Antwort**
Nach dem Bau der DP-Tabelle ist das gewünschte Maximalgewicht `dp_score[0][4] `.
Die zugehörige Indexliste `dp_list[0][4]` enthält die vier ausgewählten Intervallindizes in aufsteigender Reihenfolge.

4. **Komplexe**
*Sorting:* \(O(n\log n)\).
*DP-Schleife:* Für jedes Intervall iterieren wir über 5 Werte von *k* und führen maximal einige Vektoroperationen → \(O(n)\ aus.
*Memory:* 5 × (n + 1) 64-Bit-Nummern + 5 × (n + 1) Listen – linear in *n*.

---

oder 5. Edge Cases

* ** Multiple optimale Sets* – unsere lexicographische Regel garantiert eine einzigartige Antwort.
* ** Intervalle, die sich nicht überschneiden** – der DP wählt automatisch die vier mit den größten Gewichten aus.
* * **Sehr großer Eingang** – alle Lösungen verwenden schnelle I/O und laufen in \(O(n\log n)\) Zeit.

---

oder 6. Referenz-Implementierung – Java (vollständig kommentiert)

``java
Einfuhr java.io.*;
Import java.util.*;

Volksklasse Main {\cHFFFF}

- Nein. Datenstruktur für ein Intervall ------------- */
Private statische Klasse Interval {
int l, r, w, idx;
Interval(int l, int r, int w, int idx) {\cHFFFF}
Diese.l = l; this.r = r; this.w = w; this.idx = idx;
}
}

--------- Haupt ------------
öffentlicher statischer Leerlauf (String[] args) wirft IOException {
FastScanner fs = neuer FastScanner(System.in);
int n = fs.nextInt();
Interval[] a = neues Intervall[n];
für (in i = 0; i < n; i++) {
int l = fs.nextInt();
int r = fs.nextInt();
int w = fs.nextInt();
a[i] = new Interval(l, r, w, i); // Indizes sind 0-basiert
}

---------- Sortiert nach links Endpunkt --------------------
Arrays.sort(a, Comparator.comparingInt(o -> o.l));

/* ---------- Berechnung 'next' Array ---------------------
int[] links = neu int[n];
für (in i = 0; i < n; i++) links[i] = a[i].l;

int[] next = new int[n];
für (in i = 0; i < n; i++) {
nächstes[i] = oberer (links, a[i].r); // erstes Intervall mit L > R
}

------ DP -------------
Lang[][][ dpScore = new long[n + 1][5]; // dpScore[i][k]
Int[][[[][]] dp Liste = neu int[n + 1][5][]; // dpList[i][k] -> int[] der Indizes

für (in i = n; i >= 0; i-) { // von n-1 bis 0
für (in k = 0; k <= 4; k++) {
wenn (i == n) { // Basis: über das letzte Intervall hinaus
dpScore[i][k] = 0;
dpList[i][k] = neu int[0];
weiter;
}

/* ---- Option: aktuelles Intervall überspringen ---- */
Long skipScore = dpScore[i + 1][k];
int[] skipList = dpList[i + 1][k];

/* ---- Option: aktuelles Intervall nehmen ---- */
lange Ergebnis = a[i].w;
Int[] nehmen Liste = null;
wenn (k > 0)
nehmen Ergebnis += dpScore[next[i]][k - 1];
Int[] tmp = dpList[next[i][k - 1];
nehmen Liste = Arrays.copyOf(tmp, tmp.length + 1);
takeList[takeList.length - 1] = a[i].idx; // aktuellen Index anhängen
Arrays.sort(takeList);
} auch
// nicht nehmen, wenn k==0 (kein mehr Intervall erforderlich)
nehmen Ergebnis = Long.MIN_VALUE;
nehmen Liste = neu int[0];
}

/* ---- bessere Option (lexicographic tie) ---- */
wenn (takeScore > skipScore)
dpScore[i][k] = Take Partitur
dpList[i][k] = takeList;
} auch wenn (takeScore < skipScore)
dpScore[i][k] = skipScore;
dpList[i][k] = skipList;
} sonst { // gleiche Punkte – wählen Sie lexicographisch kleinste Liste
dpScore[i][k] = Take Ergebnis: // ein Wert
dpList[i][k] = lexicographicMin(SkipList, TakeList),
}
}
}

/* -------- Ausgang -------------------------------
int[] antwort = dpList[0][4]; // Indizes gewählter Intervalle
StringBuilder out = new StringBuilder();
für (int i = 0; i < antwort.length; i++) {
wenn (i > 0) out.append(');
aus.append(answer[i]);
}
System.out.println(out.toString());
}

/* ---------- binäre Suche: erster Index mit Wert > Schlüssel ------- */
Private statische Int obereBound(int[] arr, int key) {
int l = 0, r = arr.length;
(l < r)
int m = (l + r) >> 1;
wenn (arr[m] <= key) l = m + 1;
n = m;
}
Rückgabe l;
}

/* -------------- lexikographisch kleinste von zwei sortierten Int-Arrays */
Private statische Int[] lexicographicMin(int[] a, int[] b) {
int minLen = Math.min(a.length, b.length);
für (int i = 0; i < minLen; i++) {\cHFFFF}
wenn (a[i] != b[i]) ein[i] < b[i] ? a: b[i] zurückgibt;
}
zurück a.length <= b.length ?
}

/* --------- schnelles Scanner für Int-Eingabe --------------------------
Privat statische Klasse FastScanner {\cHFFFF}
Privater Abschluss InputStream in;
Privater Endbyte[]-Puffer = neuer Byte[1 << 16];
Int ptr = 0, len = 0;
FastScanner(InputStream in) { this.in = in; }
privat int read() wirft IOException {
wenn (ptr >= len) {
len = in.read(Puffer)
ptr = 0;
wenn (len <= 0) Rückgabe -1;
}
Rückgabepuffer[ptr++];
}
int nextInt() wirft IOException {
int c, Zeichen = 1, val = 0;
c = read(); während c <= ' -1)
wenn (c == '-') { Zeichen = -1; c = read(); }
während (c > ' ') { val = val * 10 + (c - '0'); c = read(); }
zurück val * Zeichen;
}
}
}
`` `

*Das Programm folgt genau dem oben erläuterten Algorithmus und ist mit Java 17 kompatibel. *

---

Ende des Tutorials.