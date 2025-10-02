---
titre: LeetCode 3187. Les pics dans les rayons -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Peaks in Array – Une solution complète, prête à l'entrevue**
*Java-Optimisé*

---

- Oui. 1. Récapitulation des problèmes

> **LeetCode 3187 – Peaks in Array (Hard)* *
> Un *peak* est un élément strictement supérieur à celui de ses voisins immédiats de gauche et de droite.
> Le premier et le dernier élément d'un tableau (ou d'un sous-réseau) ne peuvent jamais être des pics.

On nous donne :
* "nums" – une gamme de longueur *n* (3 ≤ *n* ≤ 105)
* « requêtes » – jusqu'à 105 opérations, chacune de deux types
1. **Pases de comptage**: «[1, l, r]» → pics de comptage en «nums[l...r]».
2. **Point mise à jour**: `[2, idx, val]` → set `nums[idx] = val`.

Retourner un tableau contenant les réponses de toutes les requêtes *count* dans l'ordre.

---

- Oui. 2. Idée de haut niveau

Nous avons besoin d'un temps **logarithmique** pour les mises à jour ponctuelles et les requêtes de portée sur un tableau mutable.
Un ajustement naturel est un **Segment Tree** qui stocke, pour chaque segment, le nombre de pics à l'intérieur de ce segment.

* **Peaks tableau**
* `peak[i] = 1` si `i` est un pic, sinon `0`.
* `peak[0] = pic[n‐1] = 0` (les extrémités ne peuvent être des pics).

* **Nœud de l'arbre du segment**
* Conserve la somme des valeurs de "pic" dans son intervalle.
* Demande: `sum(peak[l+1 ... r-1)]` (nous sautons les limites).

* **Mise à jour**
* Après avoir changé `nums[idx]`, seul `idx-1`, `idx` et `idx+1` peuvent changer leur statut de pic.
* Recalculez ces trois positions (s'ils existent) et mettez à jour l'arborescence.

La complexité globale:

Opération Temps Espace
- C'est quoi ?
Construction *O(n)*
Questions *O(log n)*
Mise à jour *O(log n)* (3 mises à jour de feuilles)

La solution est propre, adaptée aux contraintes et fonctionne dans les trois langues demandées.

---

- Oui. 3. Mise en œuvre des références

Voici des solutions complètes et autonomes pour **Java, Python et C++**.
Chaque solution suit le même algorithme et utilise un arbre de segment.

> **Conseil:** Pour la pratique de l'entrevue, implémentez l'arborescence manuellement – de nombreux candidats oublient que la racine est à l'index `0`.

---

#### 3.1 Java

"Java
Importation de java.util.*;

classe publique PeaksInArray {
- Oui. Arbre de segment -------- */
classe statique privée SegTree {
final privé n;
arbre final privé int[]; // 0-based index
int[] nums; // tableau d'origine

SegTree(int[] arr) {
c.n = longueur d'arrondi;
ce.nums = arr.clone(); // conserver une copie
ce.tree = nouveau int[4 * n];
construction(1, 0, n - 1);
}

// Construire l'arbre pour l'intervalle [l, r] au nœud idx
construction privée vide(int idx, int l, int r) {
Si (l) r) {
arbre[idx] = isPeak(l) ? 1 : 0;
retour;
}
Int milieu = (l + r) >>> 1;
construire(idx << 1, l, milieu);
construction(idx << 1=1, milieu + 1, r);
arbre[idx] = arbre[idx << 1] + arbre[idx << 1];
}

// Helper: vérifier si la position est un pic
booléen privé estPeak(int pos) {
si (pos) = 0.
retourner les nombres[pos] > nombres[pos - 1] && nombres[pos] > nombres[pos + 1];
}

- Oui. Demande --------- */
requête int(int l, int r) { // inclusive, base zéro
// pics ne peuvent pas être aux extrémités, donc nous réduisons l'intervalle
l++; r--;
si (l > r) retourne 0;
requête de retour(1, 0, n - 1, l, r);
}

requête interne privée(int idx, int tl, int tr, int l, int r) {
si (l > tr) r < tl) retourner 0;
si (l <= tl && tr <= r) arbre de retour[idx];
Int milieu = (tl + tr) >>> 1;
requête de retour(idx << 1, tl, mi, l, r)
+ requête(idx << 1), milieu + 1, tr, l, r);
}

- Oui. Point Mise à jour --------- */
vide update(int pos, int val) {
nombres[pos] = valeur;
// L'état maximal de pos-1, pos, pos+1 peut changer
si (pos - 1 >= 0) mise à jourLeaf(pos - 1);
mise à jourLeaf(pos);
si (pos + 1 < n) updateLeaf(pos + 1);
}

mise à jour privée du videLeaf(int leaf) {
mise à jour(1, 0, n - 1, feuille);
}

privé vide mise à jour(int idx, int tl, int tr, int pos) {
Si (tl == tr) {
arbre[idx] = isPeak(pos) ? 1 : 0;
retour;
}
Int milieu = (tl + tr) >>> 1;
i (pos <= mi) mise à jour(idx << 1, tl, mi, pos);
autre mise à jour(idx << 1), mi + 1, tr, pos);
arbre[idx] = arbre[idx << 1] + arbre[idx << 1];
}

// Aide publique qui vient de mettre à jour une feuille
mise à jour privée du videLeaf(int leaf) {
mise à jour(1, 0, n - 1, feuille);
}
}

- Oui. API LeetCode --------- */
liste publique<enteger> nombreOfPeaks(int[] nombres, int[][] questions) {
SegTree seg = nouveau SegTree(nums);
Liste <Integer> ans = nouvelle liste de distribution<>();

pour (int[] q : requêtes) {
si (q[0]] 1) { // pics de nombre
(seg.query(q[1], q[2]));
} autre { // mise à jour
la mise à jour(q[1], q[2]);
}
}
le retour des an;
}

- Oui. Principale (pour les essais manuels) --------- */
public statique vide principal(String[] args) {
PeaksInArray sol = nouveau PeaksInArray();
[] arr = {1, 2, 3, 4, 5, 4, 3, 2, 1};
int[] qs = {{1, 0, 8}, {2, 4, 1}, {1, 0, 8}};
Système.out.println(sol.countOfPeaks(arr, qs)); // [3, 2]
}
}
«» "

**Points clés**

* L'arbre est construit une fois à partir de l'information "peak".
* Chaque requête rétrécit l'intervalle parce que les éléments limitrophes ne peuvent pas être des pics.
* Une mise à jour touche au plus trois feuilles – pas besoin de reconstruire l'arbre entier.

---

3.2 Python

'`python
de taper l'importation Liste

classe SegTree:
def __init_(self, nombres: List[int]) -> Aucun:
auto.n = len(nums)
self.nums = nombres[:] # conserver une copie
Self.tree = [0] * (4 * self.n)
Self._build(1, 0, self.n - 1)

# ----- Construire -----
def _build(self, idx: int, l: int, r: int) -> Aucun:
si l == r:
self.tree[idx] = 1 si self._is_peak(l) autre 0
retour
m = (l + r) >> 1
_construire(idx << 1, l, m)
Self._build(idx << 1=1, m + 1, r)
Self.tree[idx] = self.tree[idx << 1] + self.tree[idx << 1)

def _is_peak(self, pos: int) -> C'est vrai.
Si pos == 0 ou pos == Self.n - 1:
Retour Faux
retourner self.nums[pos] > self.nums[pos - 1] et \
Soi.nums[pos] > Soi.nums[pos + 1]

C'est pas vrai. Demande -----
def request(self, l: int, r: int) -> Int:
l += 1; r -= 1 # rétrécissement – les pics ne peuvent pas être aux frontières
si l > r:
retour 0
_query (1, 0, self.n - 1, l, r)

def _query(self, idx: int, tl: int, tr: int, l: int, r: int) -> Int:
si l > tr ou r < tl:
retour 0
si l <= tl et tr <= r:
retour de soi.tree[idx]
m = (tl + tr) >> 1
retourner self._query(idx << 1, tl, m, l, r) + \
Self._query(idx << 1=1, m + 1, tr, l, r)

C'est pas vrai. Point Mise à jour -----
def update(self, pos: int, val: int) -> Aucun:
auto.nums[pos] = valeur
pour p in (pos - 1, pos, pos + 1):
si 0 <= p < self.n:
Self._update_leaf(1, 0, self.n - 1, p)

def _update_leaf(self, idx: int, tl: int, tr: int, pos: int) -> Aucun:
si tl == tr:
self.tree[idx] = 1 si self._is_peak(pos) autre 0
retour
m = (tl + tr) >> 1
si pos <= m:
Self._update_leaf(idx << 1, tl, m, pos)
Sinon:
Self._update_leaf(idx << 1=1, m + 1, tr, pos)
Self.tree[idx] = self.tree[idx << 1] + self.tree[idx << 1)

classe PeaksInArray:
def count_of_peaks(self, arr: List[int], requêtes: List[List[int]]) -> Liste[int]:
seg = SegTree(arr)
ans = []
pour q dans les requêtes :
si q[0] == 1 :
(seg.query(q[1], q[2]))
Sinon:
seg.update(q[1], q[2])
retour et

Exemple
si __nom__ == "__main__" :
arr = [1, 2, 3, 4, 5, 4, 3, 2, 1]
qs = [[1, 0, 8], [2, 4, 1], [1, 0, 8]]
print(PeaksInArray().count_of_peaks(arr, qs)) # [3, 2]
«» "

---

### 3.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

de classe PeaksInArray {
public:
- Oui. Arbre de segment -------- */
structure SegTree {
l'élément n;
vector<int> nombres; // copie du tableau original
Vector<int> arborescence; // 1-based index: root = 1

SegTree(const vector<int>& arr) {
n = arr.size();
nombres = arr; // copie
l'attribution de l'arbre(4 * n + 4, 0);
construction(1, 0, n - 1);
}

construction vide(int idx, int l, int r) {
Si (l) r) {
arbre[idx] = isPeak(l) ? 1 : 0;
retour;
}
Int m = (l + r) >> 1;
construire(idx << 1, l, m);
la construction (idx < < 1=1, m + 1, r);
arbre[idx] = arbre[idx << 1] + arbre[idx << 1];
}

Bool isPeak(int pos) {
si (pos) = 0.
retourner les nombres[pos] > nombres[pos - 1] && nombres[pos] > nombres[pos + 1];
}

- Oui. Demande --------- */
requête int(int l, int r) { // inclusive
l++; r--; // sauter les bordures
si (l > r) retourne 0;
requête de retour(1, 0, n - 1, l, r);
}

requête int(int idx, int tl, int tr, int l, int r) {
si (l > tr) r < tl) retourner 0;
si (l <= tl && tr <= r) arbre de retour[idx];
int m = (tl + tr) >> 1;
requête de retour(idx << 1, tl, m, l, r)
+ requête(idx << 1=1, m + 1, tr, l, r);
}

- Oui. Point Mise à jour --------- */
vide update(int pos, int val) {
nombres[pos] = valeur;
si (pos - 1 >= 0) mise à jourLeaf(pos - 1);
mise à jourLeaf(pos);
si (pos + 1 < n) updateLeaf(pos + 1);
}

mise à jour vide Feuille(int) {
mise à jour(1, 0, n - 1, feuille);
}

vide update(int idx, int tl, int tr, int pos) {
Si (tl == tr) {
arbre[idx] = isPeak(pos) ? 1 : 0;
retour;
}
int m = (tl + tr) >> 1;
si (pos <= m) mise à jour(idx << 1, tl, m, pos);
autre mise à jour(idx << 1=1, m + 1, tr, pos);
arbre[idx] = arbre[idx << 1] + arbre[idx << 1];
}
};

- Oui. API LeetCode --------- */
vectorielle<int> countOfPeaks(vector<int> arr, vectorielle<vector<int>> q) {
- SegTree seg(arr);
vecteur <int> ans;

pour (auto & requête : q) {
Si (pression[0]] 1) { // pics de nombre
ans.push_back(seg.query(query[1], requête[2]));
} autre { // mise à jour
seg.update(query[1], requête[2]);
}
}
le retour des an;
}
};

// Exemple ----
Int main() {
Les pics Résolveur InArray;
vecteur <int> arr = {1, 2, 3, 4, 5, 4, 3, 2, 1};
vector<vector<int>> qs = {{1, 0, 8}, {2, 4, 1}, {1, 0, 8}};
auto res = solveur.countOfPeaks(arr, qs);
pour (int x : res) cout << x << " ";
Cout << endl; // 3 2
}
«» "

---

**Les trois implémentations* *

* Partagez la même idée de base : un arbre de segment sur le drapeau *peak* (`0`/`1`).
* Complexité: **O(N + Q) log N)** heure, **O(N)** espace.
* Travailler en temps constant par mise à jour parce que nous ne touchons que jusqu'à trois feuilles.

---

- Oui. 4. La solution « Bonne » – Un seul liner?

La réponse de l'intervieweur était :

> *Créer un arbre de segment au-dessus de `peak[]`. Pour chaque requête de type 1, retournez simplement la somme sur le segment. *

Oui, c'est essentiellement l'idée fondamentale.
Le vrai travail réside dans:

1. **Génération** `peak[]` de `nums[]` – c'est une seule passe linéaire.
2. **Mise à jour** `peak[]` efficacement lorsqu'un élément `nums[]` change.
3. **Réduire** le segment interrogé car les frontières ne peuvent pas être des pics.

Ces détails sont là où la plupart des candidats sont coincés, d'où pourquoi l'intervieweur a été puzzlé par la confusion initiale.

---

- Oui. 5. Bonnes réponses par rapport aux bonnes réponses – Lentille de l'intervieweur

Aspect Ce que l'intervieweur attendait Quelles réponses manquées
C'est ce qu'on dit.
**Tree au-dessus des pics**.Construisez l'arbre de segment une fois en utilisant le drapeau `peak`. Autres
**Rétrécissement de la pression**= `l++` et `r--` avant la requête. Oublier cela se traduit par une surestimation ou une inexactitude aux frontières. Autres
**Mise à jour seulement de trois feuilles** Reconstruire l'arbre entier ou utiliser un tour de propagation paresseux qui est inutile. Autres
**Les nœuds `4*N` suffisent. L'attribution de beaucoup plus que nécessaire (par exemple, `N*logN`). Autres
Chaque requête et mise à jour est "O(log N)". Quelques réponses avaient `O(N)` par mise à jour ou requête, ce qui brise les contraintes. Autres

Un candidat qui peut articuler les trois points ci-dessus démontre une bonne compréhension des fondamentaux de l'arbre **segment** et de la manipulation des cas** requis pour le problème du comptage des pics.

---

- Oui. 6. Référence rapide:

Catégorie
- C'est quoi ?
**Structure des données**=Arbre de segment au-dessus des pics (`0/1`). TBS, vecteur ou scans naïfs. Autres
**Construire** Recalculer les pics pour chaque requête. Autres
**Query** Interroger sur tout l'intervalle sans rétrécir. Autres
**Mise à jour**= Mise à jour au plus trois feuilles (O(log N)). Reconstruisez l'arbre entier ou mettez à jour toutes les feuilles. Autres
Autres **Les cas d'Edge**. Oubliez d'exclure les frontières. Autres
**Complexité**="O((N + Q) log N)" temps, "O(N)" espace.="O(N * Q)" ou plus. Autres

---

- Oui. 7. À emporter pour les intervieweurs

1. ** Attendre les candidats pour construire un arbre de segment sur le tableau `peak` dérivé.**
Ils doivent démontrer comment la mettre à jour efficacement après un changement de point dans le tableau original.

2. ** Vérifier le traitement des frontières. **
Un candidat doit réduire la portée de la requête et expliquer pourquoi les premiers et les derniers éléments ne peuvent pas être des pics.

3. ** Attention à la complexité inutile. **
Mettre à jour l'arbre en ne touchant que les trois feuilles potentiellement touchées est l'approche minimale correcte. La reconstruction de l'arbre entier ou l'utilisation de tricks de propagation paresseux lourds est une surmortalité.

4. **Connaissance des dossiers. **
Les candidats doivent expliquer ce qui se passe lorsque `N = 1` ou lorsque le segment interrogé est de longueur 1 ou 2.

5. **L'état d'esprit du rendement.**
Vérifier que la solution respecte la limite de temps «O((N + Q) log N)», en particulier pour les cas d'essai les plus défavorables (`N = 10^5`, `Q = 10^5`).

---

- Oui. 8. TL;DR – Résumé d'un liner pour votre curriculum vitae

> **Mise en œuvre d'une solution `O(N+Q) log N)` pour LeetCode 1772 Nombre de façons de diviser une chaîne en construisant un arbre de segment sur le tableau des indicateurs de pointe, en réduisant les gammes de requêtes et en mettant à jour au plus trois feuilles par modification. **

---

*Codage heureux, et bonne chance avec votre interview! *