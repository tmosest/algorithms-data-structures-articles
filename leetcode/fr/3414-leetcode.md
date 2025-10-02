---
titre: LeetCode 3414. Score maximal des intervalles de non-overlaping -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

- Oui. 1. Le problème, en bref

Nous sommes donnés **N ≤ 50 000** intervalles

«» "
[li , ri , wi] (1 ≤ l ≤ ri ≤ 109, 1 ≤ wi ≤ 109)
«» "

et nous devons choisir ** au plus quatre** pour que

* pas deux intervalles choisis se touchent (l'extrémité droite de l'un doit être *strictement* plus petite que l'extrémité gauche de l'autre),
* le poids total est maximal, et
* si plusieurs sous-ensembles donnent le même poids maximal, nous retournons la liste **lexicographiquement la plus petite des indices originaux** (les indices sont basés sur 0 dans l'ordre dans lequel les intervalles apparaissent dans l'entrée).

La sortie requise est la liste des indices originaux en ordre croissant – c'est-à-dire la liste qui serait obtenue en triant simplement les indices.

> *Pourquoi au plus quatre questions* – parce que nous pouvons nous permettre une table de programmation dynamique complète avec une dimension supplémentaire **k * {0,...,4}**.
> *Pourquoi la règle de limite est importante* – le partage d'un paramètre gauche ou droit est considéré comme se chevauchant, par conséquent la condition *strict* `ri < lj` (ou vice-versa) est celle qui doit tenir.

Ci-dessous vous trouverez trois solutions de référence, une dans **Python**, une dans **Java** et une dans **C++**. Tous les trois résolvent le problème en **O(N log N)** temps et **O(N)** mémoire – confortablement dans les limites.

---

- Oui. 2. L'algorithme (même idée en trois langues)

1. ** Conserver les indices originaux**
Conservez le 4-tuple `(l, r, w, idx)` pour chaque intervalle, où `idx` est la position dans l'entrée (0-basée).

2. **Trier par le paramètre gauche**
Cela nous donne un ordre déterministe dans lequel nous allons explorer les intervalles.

3. **Pré-calculer les indices "next"**
Pour chaque intervalle `i` nous avons besoin du premier intervalle qui commence *après* `ri`.
Parce que toucher le point final est interdit, nous cherchons le plus petit `j > i` avec
"lj > ri".
L'étape de recherche binaire utilise la liste triée des extrémités de gauche.

4. ** Programmation dynamique avec une dimension supplémentaire `k`**
`dp[i][k]` = meilleur (poids, liste d'indices choisis) réalisable à partir de l'intervalle `i` lorsque nous sommes autorisés à prendre au plus `k` plus d'intervalles (`k` {0,1,2,3,4}).
La récurrence est le choix classique :

* **skip** `i` → `dp[i+1][k] "
* **Take** `i` → `wi + dp[next[i]]][k-1]` et ajouter `idxi` à la liste des indices

Parce que la liste est toujours triée et contient au plus 4 numéros, fusionner / trier la nouvelle liste est banal.

5. **Création d'un lien**
Si les deux choix donnent le même poids total, nous devons retourner la liste d'index *lexicographiquement plus petite*.
La comparaison lexicographique de deux listes d'index triées est simplement une comparaison élément par élément (par exemple, la comparaison tuple dans Python ou `std::lexicographieal_compare` dans C++).

6. **Réponse**
Démarrer la récursion (ou le DP ascendant) à partir de `i = 0` et `k = 4`.
La liste des indices qui en résulte est la réponse requise.

---

- Oui. 3. Mise en œuvre des références

3.1 Python 3

'`python
#!/usr/bin/env python3
importations
bisect d'importation
à partir de functools importer lru_cache
de taper l'importation Liste, Tuple

def max_weight_intervalles(intervalles: Liste[Liste[int]]) -> Liste[int]:
"""
Retourne la liste lexicographiquement la plus petite des indices originaux
qui donne le poids maximal en utilisant au plus 4 intervalles de non-overlaping.
"""
n = len(intervalles)
# Joindre les indices originaux et trier par point final gauche
items = [(l, r, w, idx) pour idx, (l, r, w) dans le dénombrement (intervalles)]
items.sort(key=lambda x: x[0])

starts = [x[0] pour x dans les éléments] # trié les extrémités gauches
nxt = [bisect.bisect_right(starts, items[i][1]) pour i dans l'intervalle(n)]

@lru_cache(maxsize=Aucune)
def dfs(i: int, k: int) -> Tuple[int, Tuple[int, ...]]:
""Retour (score, tuple_of_indices) de la position i avec au plus k picks."""
si k == 0 ou i == n:
retour 0, ()
♪ sauter
skip_score, skip_list = dfs(i + 1, k)

# Prise
take_score, take_list = dfs(nxt[i], k - 1)
pren_score += Éléments [i][2]
new_list = tuple(sorted(take_list + (items[i][3],))

# choisir le meilleur
si take_score > _Score de saut :
return take_score, new_list
si take_score < skip_score :
return skip_score, skip_list
# poids égal → comparaison lexicographique
retour prendre_score, min(skip_list, new_list)

best_score, best_indices = dfs(0, 4)
liste de retour(meilleures_indices)


Le conducteur...
si __nom__ == "__main__" :
données = sys.stdin.read().strip().splitlines()
si ce n'est pas des données:
sys.exit()
N = int(données[0])
intervalles = [list(map(int, line.split())) pour la ligne dans les données[1:N + 1]]
res = intervalle max_weight_(intervalles)
print(" ".join(map(str, res)))
«» "

**Explication**

* `@lru_cache` garantit que chaque paire `(i, k)` n'est calculée qu'une seule fois.
* La profondeur de récursion est limitée par `N`, mais la mise en cache empêche une explosion: seulement ~N × 5 états existent.
* "tuple(sorted(...)")" garantit que la liste est triée et prête pour la comparaison lexicographique.

---

#### 3.2 Java 17

"Java
importation java.io.*;
Importation de java.util.*;

classe publique {

classe statique privée Intervalle {
i, r, w, idx;
Intervalle(int l, int r, int w, int idx) {
ce.l = l; ce.r = r; ce.w = w; ce.idx = idx;
}
}

classe statique privée Résultat {
long score;
Liste des indices <entier>; // trié
Résultat(score long, index de la liste <entier>) {
Ça. score = score;
cet indice = indices;
}
}

Liste statique publique<entier> resoudre(Liste<int[]> brut) {
int n = brut.size();
Liste des éléments<Interval> = nouvelle liste d'éléments<>(n);
pour (int i = 0; i < n; i++) {
int[] a = cru.get(i);
éléments.add(nouveau Interval(a[0], a[1], a[2], i));
}
items.sort(Comparator.comparingInt(o -> o.l));

int[] starts = nouveau int[n];
pour (int i = 0; i < n; i++) starts[i] = items.get(i).l;
int[] suivante = nouvelle int[n];
pour (int i = 0; i < n; i++) {
int pos = upperBound(starts, items.get(i).r);
suivant[i] = pos;
}

long[][] bestScore = nouveau long[n + 1][5];
@SuppressAvertissements("non vérifié")
Liste <entier>[] bestList = nouvelle liste[n + 1][5];
pour (int k = 0; k <= 4; k++) {
bestScore[n][k] = 0;
bestList[n][k] = Collections.videList();
}

pour (int i = n - 1; i >= 0; i--) {
pour (int k = 0; k <= 4; k++) {
long skipScore = meilleurScore[i + 1][k];
Liste <entier> skipList = bestList[i + 1][k];

si (k == 0) { // rien à choisir
bestScore[i][k] = skipScore;
bestList[i][k] = skipList;
poursuivre;
}

int ni = suivant[i];
longue durée Score = items.get(i).w + bestScore[ni][k - 1];
Liste <Integer> takeList = nouvelle liste d'array<>(bestList[ni][k - 1]);
takeList.add(items.get(i).idx);
Collections.sort(TakeList);

si (prendreScore > sauterScore) {
bestScore[i][k] = prise Note;
bestList[i][k] = prise Liste;
} sinon si (takeScore < skipScore) {
bestScore[i][k] = skipScore;
bestList[i][k] = skipList;
} autre { // poids égal – rupture du lien lexicographique
bestScore[i][k] = prise Note;
bestList[i][k] = lexicographieMin(skipList, takeList);
}
}
}
retour bestList[0][4];
}

// renvoie la liste lexicographiquement plus petite de deux listes triées
liste statique privée<integer> lexicographiqueMin(liste<integer> a, liste<integer> b) {
i = 0;
pendant que (i < a.size() && i < b.size()) {
int va = a.get(i), vb = b.get(i);
si (va != vb) retourner va < vb ? a : b;
i++;
}
retourner a.size() <= b.size() ? a : b;
}

// lien supérieur sur un tableau trié
intérieur statique int upperBound(int[] arr, touche int) {
int l = 0, r = longueur d'arrondi;
pendant que (l < r) {
Int m = (l + r) >>> 1;
si (arr[m] <= clé) l = m + 1;
autres r = m;
}
retour l;
}

// --------- principal ---------
public statique vide main(String[] args) lance IOException {
BufferedReader br = nouveau BufferedReader(nouveau InputStreamReader(System.in));
int n = Integer.parseInt(br.readLine().trim());
Liste<int[]> brut = nouvelle liste de distribution<>();
pour (int i = 0; i < n; i++) {
Chaîne[] parties = br.readLine().trim().split("\\s+");
rough.add(new int[]{Integer.parseInt(parties[0]),
Integer.parseInt(parties[1]),
(parties[2])
}
Liste <entier> ans = resoudre(raw);
StringBuilder sb = nouveau StringBuilder();
pour (int i = 0; i < ans.size(); i++) {
si (i > 0) sb.append('');
sb.append(ans.get(i));
}
Système.out.println(sb);
}
}
«» "

**Points clés* *

* `@lru_cache` garantit O(1) par État.
* `min(skipList, newList)` utilise la comparaison de tuple – le tuple lexicographiquement plus petit est automatiquement choisi lorsque les poids totaux sont égaux.

---

#### 3.3 Java 17 (PDD ascendant – pas de récursion)

"Java
importation java.io.*;
Importation de java.util.*;

classe publique {
classe statique privée Intervalle {
i, r, w, idx;
Intervalle(int l, int r, int w, int idx) {
ce.l = l; ce.r = r; ce.w = w; ce.idx = idx;
}
}

liste statique privée<enteger> résolvez(Liste<int[]> brut) {
int n = brut.size();
Liste des éléments<Interval> = nouvelle liste d'éléments<>(n);
pour (int i = 0; i < n; i++) {
int[] a = cru.get(i);
éléments.add(nouveau Interval(a[0], a[1], a[2], i));
}
items.sort(Comparator.comparingInt(o -> o.l));

int[] starts = nouveau int[n];
pour (int i = 0; i < n; i++) starts[i] = items.get(i).l;
int[] suivante = nouvelle int[n];
pour (int i = 0; i < n; i++) {
next[i] = upperBound(starts, items.get(i).r);
}

long[][] bestScore = nouveau long[n + 1][5];
@SuppressAvertissements("non vérifié")
Liste <entier>[] bestList = nouvelle liste[n + 1][5];
pour (int k = 0; k <= 4; k++) {
bestScore[n][k] = 0;
bestList[n][k] = Collections.videList();
}

pour (int i = n - 1; i >= 0; i--) {
pour (int k = 0; k <= 4; k++) {
// sauter
long skipScore = meilleurScore[i + 1][k];
Liste <entier> skipList = bestList[i + 1][k];

si (k == 0) { // rien d'autre à prendre
bestScore[i][k] = skipScore;
bestList[i][k] = skipList;
poursuivre;
}

// prise
int ni = suivant[i];
longue durée Score = items.get(i).w + bestScore[ni][k - 1];
Liste <Integer> takeList = nouvelle liste d'array<>(bestList[ni][k - 1]);
takeList.add(items.get(i).idx);
Collections.sort(TakeList);

si (prendreScore > sauterScore) {
bestScore[i][k] = prise Note;
bestList[i][k] = prise Liste;
} sinon si (takeScore < skipScore) {
bestScore[i][k] = skipScore;
bestList[i][k] = skipList;
} autres { // poids égal – lexicographie min
bestScore[i][k] = prise Note;
bestList[i][k] = lexicographieMin(skipList, takeList);
}
}
}
retour bestList[0][4];
}

// limite supérieure sur les paramètres triés à gauche
intérieur statique int upperBound(int[] arr, touche int) {
int l = 0, r = longueur d'arrondi;
pendant que (l < r) {
Int m = (l + r) >>> 1;
si (arr[m] <= clé) l = m + 1;
autres r = m;
}
retour l;
}

// renvoie la liste lexicographiquement plus petite de deux listes triées
liste statique privée<integer> lexicographiqueMin(liste<integer> a, liste<integer> b) {
i = 0;
pendant que (i < a.size() && i < b.size()) {
int va = a.get(i), vb = b.get(i);
si (va != vb) retourner va < vb ? a : b;
i++;
}
retourner a.size() <= b.size() ? a : b;
}

public statique vide main(String[] args) lance IOException {
BufferedReader br = nouveau BufferedReader(nouveau InputStreamReader(System.in));
int n = Integer.parseInt(br.readLine().trim());
Liste <int[]> brut = nouvelle liste d'array<>(n);
pour (int i = 0; i < n; i++) {
Chaîne[] parties = br.readLine().trim().split("\\s+");
rough.add(new int[]{Integer.parseInt(parties[0]),
Integer.parseInt(parties[1]),
(parties[2])
}
Liste <entier> ans = resoudre(raw);
StringBuilder sb = nouveau StringBuilder();
pour (int i = 0; i < ans.size(); i++) {
si (i > 0) sb.append('');
sb.append(ans.get(i));
}
Système.out.println(sb);
}
}
«» "

**Pourquoi en haut? **

* Récursion avec mémoisation pourrait également fonctionner, mais un DP itératif simple élimine tout risque de débordement de pile et est très simple à comprendre.

---

3.4 Python 3 (autre forme courte)

'`python
résoudre():
importations
données = sys.stdin.read().strip().split()
si ce n'est pas des données:
retour
it = iter(données)
n = int(next(it))
brut = [(int(next(it)), int(next(it)), int(next(it))) pour _ dans l'intervalle(n)]
rough.sort(key=lambda x: x[0]) # trier par point final gauche

début = [x[0] pour x en brut]
def upper_bound(a, clé):
l, r = 0, len(a)
alors que l < r:
m = (l + r) >> 1
si a[m] <= clé: l = m + 1
autres: r = m
retour l

next_idx = [upper_bound(starts, x[1]) pour x en brut]
dp_score = [[0]*5 pour _ dans l'intervalle(n+1)]
dp_list = [[[]]*5 pour _ dans l'intervalle(n+1)]
pour i dans la plage(n-1, -1, -1):
pour k dans la plage(5):
skip_score = dp_score[i+1][k]
skip_list = dp_list[i+1][k]
Si k==0:
dp_score[i][k] = skip_score
dp_list[i][k] = skip_list
poursuivre
take_score = brut[i][2] + dp_score[next_idx[i][k-1]
take_list = trié(dp_list[next_idx[i]][k-1] + [i])
si take_score > _Score de saut :
dp_score[i][k] = take_score; dp_list[i][k] = take_list
elif take_score < skip_score:
dp_score[i][k] = skip_score; dp_list[i][k] = skip_list
Autre: # poids égal
dp_score[i][k] = take_score
dp_list[i][k] = min(skip_list, take_list)
print(' '.join(map(str, dp_list[0][4]))
«» "

---

*## 3.5 C++ 17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

struct Intervalle {
i, r, w, idx;
};

int upperBound(vecteur commun<int>&a, clé int) {
Int l = 0, r = (int)a.size();
pendant que (l < r) {
Int m = (l + r) >> 1;
si (a[m] <= clé) l = m + 1;
autres r = m;
}
retour l;
}

Int main() {
ios::sync_with_stdio(faux);
cin.tie (nullptr);
l'élément n;
si (!(cin >> n)) retourner 0;
vecteur <Interval> v;
pour (int i = 0; i < n; ++i) {
i, r, w; cin >> l >> r >> w;
v.emplace_back(l, r, w, i);
}
tri(v.begin(), v.end(), [](const Interval& a, const Interval& b){ retour a.l < b.l; });

le vecteur<int> commence(n);
pour (int i = 0; i < n; ++i) début[i] = v[i].l;
vecteur<int> nxt(n);
pour (int i = 0; i < n; ++i) nxt[i] = upperBound(starts, v[i].r);

vecteur<array<long long,5>> score(n+1);
vecteur<array<vector<int>,5>> lst(n+1);
pour (int k = 0; k <= 4; ++k) {
score[n][k] = 0;
lst[n][k] = {};
}

pour (int i = n-1; i >= 0; --i) {
pour (int k = 0; k <= 4; ++k) {
long sautS = score[i+1][k];
le vecteur const<int>& skipL = lst[i+1][k];

si (k) 0) {
score[i][k] = sautS;
lst[i][k] = skipL;
poursuivre;
}

longue duréeS = v[i].w + score[nxt[i]][k-1];
vecteur<int> takeL = lst[nxt[i][k-1];
takeL.push_back(v[i].idx);
tri(takeL.begin(), takeL.end());

si (prise > saute) {
score[i][k] = priseS;
lst[i][k] = takeL;
} sinon si (takeS < skipS) {
score[i][k] = sautS;
lst[i][k] = skipL;
} autre {
// égal – lexicographie min
score[i][k] = priseS;
// min lexicographique de deux vecteurs triés
Const vector<int>& a = skipL, &b = takeL;
vecteur<int> res = a;
bool moins = faux;
pour (size_t t = 0; t < min(a.size(), b.size()); ++t) {
si (a[t] != b[t]) {
moins = a[t] < b[t];
pause;
}
}
si (moins) res = a;
sinon si (a.size() > b.size()) res = b;
lst[i][k] = res;
}
}
}
pour (size_t i = 0; i < lst[0][4].size(); ++i) {
si i) cout << ' ';
cout << lst[0][4][i];
}
Cout << '\n';
}
«» "

** Faits saillants* *

* Utilise `vector<array<>>` pour les tableaux DP (taille fixe 5 pour `k`).
* La comparaison lexicographique se fait manuellement avec une petite boucle.

---

C'est pas vrai.

C'est vrai.
utiliser le système;
utilisant le système. Recouvrements. générique;
utilisant le système. OI;
utilisant le système. Linq;

Programme de classe publique
{
enregistrement privé Interval(int L, int R, int W, int Id);

le résultat du dossier privé (long score, liste<int> indices);

vide statique public Main()
{
var input = Console.ReadLine();
si (entrée == null) retour;
int n = int.Parse(input);
var cru = nouvelle liste<int[]>();
pour (int i = 0; i < n; i++)
{
var parts = Console.ReadLine().Split(', StringSplitOptions.SupprimerEmptyEntries);
brut. Ajouter(new int[] { int.Parse(parts[0]), int.Parse(parts[1]), int.Parse(parts[2]) };
}

var ans = Solve(raw);
Console.WriteLine(string.Join(', ans));
}

Liste statique privée<int> Solve(Liste<int[]> brute)
{
int n = brut. Compte;
var items = nouvelle liste<Interval>(n);
pour (int i = 0; i < n; i++)
Éléments. Ajouter(nouveau Interval(raw[i][0], brut[i][1], brut[i][2], i));

items.Sort(a, b) => a.L.CompareTo(b.L)

int[] starts = items.Select(x => x.L).ToArray();
int[] suivante = nouvelle int[n];
pour (int i = 0; i < n; i++)
next[i] = UpperBound(départ, items[i].R);

long[][] bestScore = nouveau long[n + 1];
Liste<int>[][] bestList = nouvelle liste<int>[n + 1];
pour (int k = 0; k <= 4; k++)
{
bestScore[n] = nouveau long[5];
bestList[n] = nouvelle liste<int>[5];
pour (int kk = 0; kk <= 4; kk++)
{
bestScore[n][kk] = 0;
bestList[n][kk] = nouvelle liste<int>();
}
}

pour (int i = n - 1; i >= 0; i--)
{
pour (int k = 0; k <= 4; k++)
{
long skipScore = meilleurScore[i + 1][k];
Liste<int> skipList = bestList[i + 1][k];

si (k) 0)
{
bestScore[i][k] = skipScore;
bestList[i][k] = skipList;
poursuivre;
}

longue durée Note = éléments[i]. W + bestScore[next[i]][k - 1];
var takeList = nouvelle liste<int>(bestList[next[i]][k - 1]) { items[i]. Numéro d'identification
takeList.Sort();

si (prendre le score > sauter le score)
{
bestScore[i][k] = prise Note;
bestList[i][k] = prise Liste;
}
Sinon, si (takeScore < skipScore)
{
bestScore[i][k] = skipScore;
bestList[i][k] = skipList;
}
autre // poids égal
{
bestScore[i][k] = prise Note;
// min lexicographique
bestList[i][k] = LexicographicMin(skipList, takeList);
}
}
}
retour bestList[0][4];
}

Int statique privé UpperBound(int[] a, touche int)
{
int l = 0, r = a.longueur;
pendant que (l < r)
{
int m = (l + r) / 2;
si (a[m] <= clé) l = m + 1;
autres r = m;
}
retour l;
}

Liste statique privée<int> Min(Liste<int> a, Liste<int> b)
{
int len = Math.Min(a.Count, b.Count);
pour (int i = 0; i < len; i++)
{
si (a[i] != b[i]) retourne a[i] < b[i] ? a : b;
}
retour a.Count <= b.Count ? a : b;
}
}
«» "

* C# 11 utilise l'"enregistrement" pour la brièveté et les structures de données immuables.

---

- Oui. 4. Explication de l'algorithme (programmation dynamique)

1. **Désolé**
Tous les intervalles sont triés par le paramètre de gauche \(L_i\).
Cela garantit que si l'intervalle *j* commence après *i* (\(L_j > L_i\), alors dans l'ordre trié *j* apparaîtra après *i*.
La propriété nécessaire pour la récurrence DP est:
*L'intervalle le plus droit qui se termine avant le point final gauche de l'intervalle courant est le précédent. *
Parce que les intervalles sont triés par *L*, ce prédécesseur peut être trouvé avec une recherche binaire sur le tableau des paramètres de gauche.

2. ** Programmation dynamique**
Pour chaque position *i* (intervalle *i*) et pour chaque nombre *k* d'intervalles déjà choisis (\(0\le k\le 4\)) nous stockons:
* `dp_score[i][k]` – poids total maximal réalisable compte tenu uniquement des intervalles avec des indices ≥ i lorsque des intervalles *k* ont déjà été choisis.
* `dp_list[i][k]` – la liste des indices triée correspondante.

Récurrence pour l'intervalle *i* (0-based index):

«» "
skip: ne choisissez rien de l'intervalle i
score = dp_score[i+1][k]
liste = dp_list[i+1][k]

prendre: choisir l'intervalle i (ne doit pas se chevaucher avec l'intervalle choisi ultérieurement)
let p = next_index[i] // premier intervalle commençant après R_i
score = poids[i] + dp_score[p][k-1]
liste = triée( dp_list[p][k-1]
«» "

Si les deux scores diffèrent, nous gardons le plus grand.
Si les scores sont égaux, nous conservons la liste d'index *lexicographiquement la plus petite* – c'est ce que demande l'énoncé.

3. **Réponse**
Une fois la table DP construite, le poids maximal souhaité est `dp_score[0][4]`.
La liste d'index associée `dp_list[0][4]` contient les quatre indices d'intervalle sélectionnés en ordre ascendant.

4. **Complexités**
*Trier:* \(O(n\log n)\).
*Loop PD:* Pour chaque intervalle nous itérerons plus de 5 valeurs de *k* et effectuerons au maximum quelques opérations vectorielles → \(O(n)\).
*Mémoire:* 5 × (n + 1) numéros 64 bits + 5 × (n + 1) listes – linéaire en *n*.

---

- Oui. 5. Cas de bord

* **Plusieurs ensembles optimaux** – notre règle lexicographique garantit une réponse unique.
* ** Intervalles qui ne se chevauchent pas** – le DP sélectionne automatiquement les quatre avec des poids plus importants.
* **Très grande entrée** – toutes les solutions utilisent des E/S rapides et fonctionnent dans le temps \(O(n\log n)\).

---

- Oui. 6. Mise en œuvre des références – Java (avec commentaires)

"Java
importation java.io.*;
Importation de java.util.*;

classe publique {

- Oui. structure des données pour un intervalle
classe statique privée Intervalle {
i, r, w, idx;
Intervalle(int l, int r, int w, int idx) {
ce.l = l; ce.r = r; ce.w = w; ce.idx = idx;
}
}

/* ---------- ------------------------------------- */
public statique vide main(String[] args) lance IOException {
FastScanner fs = nouveau FastScanner (System.in);
int n = fs.nextInt();
Intervalle[] a = nouveau Interval[n];
pour (int i = 0; i < n; i++) {
int l = fs.nextInt();
int r = fs.nextInt();
int w = fs.nextInt();
a[i] = nouvelle Interval(l, r, w, i); // les indices sont basés sur 0
}

/* --------- trier par point final gauche ------------------- */
les tableaux.sort(a, Comparator.comparingInt(o -> o.l));

/* ----------calculer le tableau « suivant » -------------------- */
int[] gauches = nouvelle int[n];
pour (int i = 0; i < n; i++) gauches[i] = a[i].l;

int[] suivante = nouvelle int[n];
pour (int i = 0; i < n; i++) {
next[i] = upperBound(gauches, a[i].r); // premier intervalle avec L > _Ri
}

- Oui. PDD -------------------------------------- */
long[][] dpScore = nouveau long[n + 1][5]; // dpScore[i][k]
[]][] dp Liste = nouvelle int[n + 1][5]; // dpList[i][k] -> int[] des indices

pour (int i = n; i >= 0; i--) { // de n-1 à 0
pour (int k = 0; k <= 4; k++) {
si (i == n) { // base: au-delà du dernier intervalle
dpScore[i][k] = 0;
dpList[i][k] = nouvelle int[0];
poursuivre;
}

/* ----- option: sauter l'intervalle actuel ----- */
long skipScore = dpScore[i + 1][k];
Int[] skipList = dpList[i + 1][k];

/* ----- option: prendre l'intervalle courant ----- */
longue durée Score = a[i].w;
prise Liste = null;
si (k > 0) { // nous ne pouvons prendre que si nous avons encore besoin d'intervalles
prise Note += dpScore[next[i]][k - 1];
int[] tmp = dpList[next[i]][k - 1];
prise Liste = Arrays.copyOf(tmp, tmp.longueur + 1);
takeList[takeList.longueur - 1] = a[i].idx; // annexer l'index actuel
Tableaux.sort(TakeList);
} autre {
// ne peut pas prendre quand k==0 (plus d'intervalles nécessaires)
prise Score = Long.MIN_VALUE;
prise Liste = nouvelle int[0];
}

/* ----- choisir une meilleure option (attache lexicographique) ----- */
si (prendreScore > sauterScore) {
dpScore[i][k] = prise Note;
dpList[i][k] = takeList;
} sinon si (takeScore < skipScore) {
dpScore[i][k] = skipScore;
dpList[i][k] = skipList;
} autre { // scores égaux – choisissez la liste laxicographiquement la plus petite
dpScore[i][k] = prise Note; // même valeur
dpList[i][k] = lexicographieMin(skipList, takeList);
}
}
}

Sortie --------------------------------- */
réponse int[] = dpList[0][4]; // indices des intervalles choisis
StringBuilder out = nouveau StringBuilder();
pour (int i = 0; i < response.longueur; i++) {
si (i > 0) out.append('');
out.append(réponse[i]);
}
Système.out.println(out.toString());
}

/* --------- recherche binaire: premier indice avec valeur > touche ------- */
intérieur statique int upperBound(int[] arr, touche int) {
int l = 0, r = longueur d'arrondi;
pendant que (l < r) {
Int m = (l + r) >>> 1;
si (arr[m] <= clé) l = m + 1;
autres r = m;
}
retour l;
}

/* --------- lexicographiquement plus petit de deux tableaux d'entrée triés */
interne statique privée[] lexicographieMin(int[] a, int[] b) {
int minLen = Math.min(a.longueur, b.longueur);
pour (int i = 0; i < minLen; i++) {
si (a[i] != b[i]) retourne a[i] < b[i] ? a : b;
}
retour a.longueur <= b.longueur ? a : b;
}

/* --------- scanner rapide pour entrée int ------------------------ */
classe statique privée FastScanner {
entrée finale privée;
octet final privé[] tampon = nouvel octet[1 << 16];
Int privé ptr = 0, len = 0;
FastScanner(InputStream in) { this.in = in; }
privé int read() lance IOException {
si (ptr >= len) {
len = in.read(buffer);
ptr = 0;
si (len <= 0) retour -1;
}
retour du tampon[ptr++];
}
int nextInt() lance IOException {
int c, signe = 1, val = 0;
do c = read(); while (c <= ' && c != -1);
si c == '-') { signe = -1; c = read(); }
(c > ' ) { val = val * 10 + (c - ' 0 '); c = read(); }
val de retour * signe;
}
}
}
«» "

*Le programme suit exactement l'algorithme expliqué ci-dessus et est compatible avec Java 17. *

---

Fin du tutorial.