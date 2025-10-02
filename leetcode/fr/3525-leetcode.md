---
titre: LeetCode 3525. Trouver la valeur X de Array II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

- Oui. 1. Le problème (Code de bord 3525)

> **Trouver la valeur X d'Array II (Hard)* *
> On vous donne un tableau entier `nums`, un entier `k` et un tableau 2-D `queries`.
> Pour chaque requête `[idx, val, start, x]` vous devez
> 1. Remplacer «nums[idx]» par «val».
> 2. Supprimer le préfixe `nums[0 ... start‐1]`.
> 3. À partir du suffixe restant `nums[départ ... n‐1]` vous pouvez **supprimer tout suffixe** – cela équivaut à **choisir tout préfixe non vide de ce suffixe**.
> Compter combien de préfixes de ce type ont un produit qui est congruent à `x (mod k)` et retourner ce numéro.
> Retourner un tableau entier `ans` où `ans[i]` est la réponse pour la requête *i‐th*.
> Contraintes: `1 ≤ longueur nominale ≤ 105`, `1 ≤ k ≤ 5`, `1 ≤ longueur de requêtes ≤ 105`.

L'observation clé est qu'après le lancement des premiers éléments "démarrage", la seule opération légale est *choisir un préfixe non vide de la sous-tribu restante*.
Donc pour chaque requête nous avons besoin du nombre de préfixes du segment `nums[démarrer ... n‐1]` dont le produit est "x (mod k)".
Nous devons prendre en charge **point updates** et **range prefix requêtes** – un cas d'utilisation classique pour un arbre de segment.



-----------------------------------------------------------------------------------

- Oui. 2. L'idée fondamentale – Arbre segmenté de préfixes-remains

Concept Ce que le nœud stocke Pourquoi il est suffisant
- Non, non, non.
Produit "prod" de **tous** éléments dans le segment des nœuds, modulo réduit Nous avons besoin de combiner les restes lorsque nous préparons un enfant de gauche à un enfant de droite. Autres
Le nombre de préfixes **non vides** à l'intérieur du segment des nœuds dont le produit "r (mod k)"" nous donne exactement ce dont nous avons besoin lorsque nous fusionnons deux enfants – tous les préfixes se trouvent entièrement dans l'enfant gauche ou commencent dans l'enfant gauche et continuent dans l'enfant droit. Autres

**Merge deux enfants (`L` puis `R`)* *

«» "
fusion.prod = (L.prod * R.prod) % k

fusion.cnt = L.cnt // préfixes qui restent entièrement dans L
pour chaque r en 0 ... k- 1
si R.cnt[r] > 0
nouveau_r = (L.prod * r) % k
fusionned.cnt[new_r] += R.cnt[r]
«» "

Ceci est `O(k)` par fusion et `k ≤ 5`, il est donc temps constant.



-----------------------------------------------------------------------------------

- Oui. 3. Algorithme

1. **Construire** l'arbre du segment dans le temps "O(nk)".
Les feuilles stockent `cnt[ nums[i] % k ] = 1` et `prod= nums[i] % k'.
Les nœuds internes sont construits par la règle de fusion ci-dessus.

2. **Pour chaque requête** `[idx, val, start, x]`
* **Mise à jour** la feuille à `idx` avec la nouvelle valeur `val`.
* **Query** l'arborescence du segment sur `[start, n-1]` (inclus).
* La requête retourne un noeud; la réponse est `node.cnt[x]`.

3. **Retour** le tableau de réponses.



-----------------------------------------------------------------------------------

- Oui. 4. Preuve d ' exactitude

Nous prouvons que l'algorithme renvoie la bonne réponse pour chaque requête.

---

Lemma 1
Pour tout nœud `v` représentant le segment `S`, `v.cnt[r]` est égal au nombre de préfixes **non vides** de `S` dont le produit est conforme à `r (mod k)`.

**Prof.**
Induction sur la hauteur du nœud.

*Base (feuille)* – une feuille contient un seul élément `a`.
Le seul préfixe non vide est l'élément lui-même, dont le produit modulo `k` est `a % k`.
Ainsi, `cnt[a % k] = 1` et tous les autres compteurs sont `0`, satisfaisant au lemma.

*Étape d'induction* – Supposons que la lemma soit retenue pour les deux enfants `L` et `R`.
Let `S = L ' R '.
Chaque préfixe non vide de `S` est soit
* un préfixe entièrement à l ' intérieur de `L` (contributeur `L.cnt[r]`), ou
* l'ensemble «L» suivi d'un préfixe «R».
Pour le deuxième cas, un préfixe de `R` avec le reste `r2` devient un préfixe de `S` avec le reste `(L.prod * r2) % k`.
Exactement cette logique est utilisée dans la procédure de fusion, de sorte que le tableau résultant `cnt` contient les comptes corrects pour `S`.



Lemma 2
Pour tout segment `[l, r]`, la routine de requête renvoie un noeud dont le tableau `cnt` est égal au nombre de préfixes de `nums[l ... r]` avec chaque reste, et dont `prod` est égal au produit du segment entier modulo `k`.

**Prof.**
La routine de requête regroupe les nœuds de gauche à droite en utilisant la même règle de fusion que l'étape de construction.
Comme la fusion est associative (prouvée par Lemma 1), le nœud final fusionné représente exactement la concaténation de tous les sous-segments qui couvrent `[l, r]`.
Par conséquent, son tableau `cnt` contient les nombres désirés et son `prod` est correct. *



- Oui. Théorème
Pour chaque requête `[idx, val, start, x]` l'algorithme produit le nombre de façons de supprimer un suffixe du sous-array `nums[start ... n-1]` après le remplacement de `nums[idx]` par «val» de telle sorte que le préfixe restant ait le produit «x (mod k)».

**Prof.**
Après la mise à jour, l'arborescence du segment reflète correctement le nouveau tableau de Lemma 1.
La requête sur `[start, n-1]` donne, par Lemma 2, le nombre de tous les préfixes de ce suffixe.
Choisir un préfixe de longueur `l` équivaut à enlever un suffixe de longueur `n - start - l`.
Ainsi, chaque opération autorisée correspond exactement à un préfixe compté, et inversement.
La réponse est donc `node.cnt[x]`, qui est ce que l'algorithme retourne. *



-----------------------------------------------------------------------------------

- Oui. 5. Analyse de la complexité

Étape Temps Espace
C'est pas vrai.
Construire (chaque noeud stocke un tableau de la taille `k`) Autres
Point Mise à jour de l'élément O(k · log n) supplémentaire
O(k · log n) supplémentaire

Avec `k ≤ 5`, la constante cachée est minuscule – la solution satisfait facilement les limites du LeetCode.



-----------------------------------------------------------------------------------

- Oui. 6. Mise en œuvre des références

Vous trouverez ci-dessous le code complet pour Java, Python et C++ qui correspond à l'API LeetCode.

> **Note** – Dans les environnements Java et C++ de LeetCode, la classe doit être appelée `Solution` et la méthode publique.
> Dans Python, la fonction `resultArray` doit être un membre de la classe `Solution`.

---

#### 6.1 C++ (GNU C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
int k, n, taille; // k ≤ 5
vector<int> prod; // prod à chaque noeud d'arbre
vecteur<array<int, 6>> cnt; // cnt[rem] à chaque noeud (index 0...k-1 utilisé)

// fusionner deux nœuds enfants aux positions l, r en parent p
fusion de vide(int p, int l, int r) {
prod[p] = (prod[l] * prod[r]) % k;
pour (int i = 0; i < k; ++i) cnt[p]i] = cnt[l]i];
pour (int rem = 0; rem < k; ++ rem) {
si (cnt[r][rem]) {
int newrem = (prod[l] * rem) % k;
cnt[p][newRem] += cnt[r][rem];
}
}
}

public:
vector<int> resultArray(vector<int>& nums, int k_, vector<vector<int>& requêtes) {
k = k_;
n = nombres.size();
taille = 1;
pendant que (taille < n) taille <<= 1; // puissance de deux ≥ n

l'attribution de prod.(2 * taille, 0);
cnt.assign(2 * taille, tableau<int, 6>{0});

// ----- construire des feuilles -----
pour (int i = 0; i < n; ++i) {
int pos = taille + i;
prod[pos] = nombres[i] % k;
cnt[pos][prod[pos]] = 1;
}

// ----- construire des nœuds internes -----
pour (int i = taille - 1; i >= 1; --i) fusionner(i, i << 1, i << 1);

vecteur <int> ans;
as.reserve(queries.size());

// ----- requêtes relatives au processus -----
pour (auto &q : requêtes) {
int idx = q[0];
Int val = q[1];
début int = q[2];
int x = q[3];

// Mettre à jour la feuille
int pos = taille + idx;
prod[pos] = valeur % k;
cnt[pos].fill(0);
cnt[pos][prod[pos]] = 1;
// Mettre à jour les parents
pour (pos >>= 1; pos; pos >>= 1) fusionner(pos, pos << 1, pos << 1-);

// requête sur [start, n-1]
int l = début + taille, r = (n - 1) + taille;
int resProd = 1; // sera écrasé
tableau <int, 6> resCnt{};
bool first = true;

// requête itérative (deux piles – gauche & droite)
Tir automatique = [&](int &p) {
si (premier) {
resProd = prod[p];
resCnt = cnt[p];
premier = faux;
} autre {
int tmpProd = res Produit;
La présente décision entre en vigueur le jour suivant celui de sa publication au Journal officiel de l'Union européenne.
memcpy(tmpCnt, resCnt.data(), taille de(int)*6);
// fusionner tmpCnt (à gauche) avec cnt[p] (à droite)
int newProd = (tmpProd * prod[p]) % k;
tableau <int, 6> newCnt = tmpCnt;
pour (int rem = 0; rem < k; ++ rem) {
si (cnt[p][rem]) {
int newRem = (tmpProd * rem) % k;
nouvelleCnt[newRem] += cnt[p][rem];
}
}
rés Prod = nouveauProd;
rés Cnt = nouveauCnt;
}
};

pendant que (l <= r) {
si (l & 1) tire(l++);
si (!(r & 1)) tire(r--);
Le nombre d'heures de travail est égal à celui des heures de travail. 1;
r >>= 1;
}

ans.push_back(resCnt[x]);
}
le retour des an;
}
};
«» "

---

#### 6.2 Python 3 (PyPy 3.7)

'`python
Numéro de classe:
__slots__ = ('cnt', 'prod')
def __init_(self, k):
auto.cnt = [0] * k
auto.prod = 0


Catégorie Arbre :
def __init_(self, nums, k):
Self.k = k
auto.n = len(nums)
taille de soi = 1
alors que moi. taille < auto.n:
taille de soi <<= 1
self.tree = [Node(k) pour _ dans la plage(2 * self.size)]
auto.construction(nombres)

Def build(self, nombres):
♪ feuilles
pour i à portée(self.n):
noeud = self.tree[self.size + i]
val = nombres[i] % self.k
noeud.prod = valeur
node.cnt[val] = 1
# noeuds internes
pour i dans la gamme (self.size - 1, 0, -1):
Self.pull(i)

def pull(self, i):
gauche, droite = self.tree[i << 1], self.tree[i << 1=1]
noeud = self.tree[i]
node.prod = (gauche.prod * droite.prod) % self.k
node.cnt = gauche.cnt[:] # Reçu
pour r dans la plage (self.k):
Si c'est vrai. [r]:
new_r = (left.prod * r) % self.k
Node.cnt[new_r] += right.cnt[r]

def update(self, pos, val):
i = taille de soi + pos
noeud = self.tree[i]
node.prod = valeur % self.k
noeud.cnt = [0] * Self.k
node.cnt[node.prod] = 1
* = 1
alors que i:
Self.pull(i)
* = 1

def requête(self, l, r):
l += taille de soi
r += taille de soi
_Node gauche = Aucun
_noeud droit = Aucun
alors que l <= r:
si l & 1:
si le _noeud gauche n'est pas :
_noeud gauche = self.tree[l]
Sinon:
gauche_node = self._merge(left_node, self.tree[l])
l += 1
si non r & 1:
si le _noeud droit n'est pas :
right_node = self.tree[r]
Sinon:
right_node = self._merge(self.tree[r], right_node)
r -= 1
Le nombre d'heures de travail est égal à celui des heures de travail. 1
r >>= 1
si le _noeud gauche n'est pas :
_nœud droit de retour
si le _noeud droit n'est pas :
retourner le _noeud gauche
return self._merge(left_node, droite_node)

def _merge(self, gauche, droite):
noeud = noeud(self.k)
node.prod = (gauche.prod * droite.prod) % self.k
node.cnt = gauche.cnt[:]
pour r dans la plage (self.k):
Si c'est vrai. [r]:
new_r = (left.prod * r) % self.k
Node.cnt[new_r] += right.cnt[r]
noeud de retour


Solution de classe:
Résultat Array(self, nombres: List[int], k: int,
questions : Liste[List[int]]) -> Liste[int]:
m = SegmentTree(nums, k)
ans = []
pour idx, val, start, x dans les requêtes:
st.update(idx, val)
noeud = st.query(départ, len(nums) - 1)
Annexe(node.cnt[x])
retour et
«» "

---

### 6.3 Java (Java 17)

"Java
Importation de java.util.*;

solution de classe {
Numéro de classe statique {
d'autre part,
[] cnt;
Node(int k) { cnt = nouvelle int[k]; }
}

classe statique SegTree {
int n, k, taille;
Arbre de nœud; // 1-basé, taille 2*

SegTree(int[] nums, int k) {
k = k;
ce.n = longueur nums;
taille = 1;
pendant la taille (taille < n) <<= 1;
arbre = nouveau nœud[2 * taille];
pour (int i = 0; i < 2 * taille; i++) arbre[i] = nouveau nœud(k);
build(nums);
}

vide build(int[] nums) {
// feuilles
pour (int i = 0; i < n; i++) {
int pos = taille + i;
Int val = nombres[i] % k;
arbre[pos].prod = valeur;
arbre[pos].cnt[val] = 1;
}
// noeuds internes
pour (int i = taille - 1; i >= 1; --i) traction(i);
}

tirant vide(int idx) {
Noeud gauche = arbre[idx << 1];
Noeud droit = arbre[idx << 1=1];
Cur = arbre[idx];
cur.prod = (gauche.prod * droite.prod) % k;
les tableaux.fill(cur.cnt, 0);
Système.arraycopy(gauche.cnt, 0, cur.cnt, 0, k);
pour (int r = 0; r < k; ++r) {
si (droite.cnt[r] > 0) {
int newR = (gauche.prod * r) % k;
cur.cnt[newR] += right.cnt[r];
}
}
}

vide update(int pos, int val) {
pos = taille + pos;
arbre[pos]. prod = valeur % k;
Arrays.fill(tree[pos].cnt, 0);
arbre[pos].cnt[tree[pos].prod] = 1;
pos >>= 1;
pendant que (pos >= 1) { pull(pos); pos >>= 1; }
}

requête node(int l, int r) { // inclusivement
l += taille; r += taille;
Noeud gauche Res = nul, droit Res = nul;
pendant que (l <= r) {
si ((l & 1)] 1) {
gauche Res = (leftRes == null) ? arbre[l] : fusion(gaucheRes, arbre[l]);
l++;
}
si ((r & 1)] 0) {
rightRes = (rightRes == null) ? arbre[r] : fusion(tree[r], droitRes);
R--;
}
L >>= 1; r >>= 1;
}
si (leftRes == null) retourner le droitRes;
si (rightRes == null) retourner à gauche Rés;
retour merge(leftRes, rightRes);
}

Fusion de nœud(Node gauche, Node droite) {
Nœud res = nouveau Nœud(k);
res.prod = (left.prod * right.prod) % k;
res.cnt = gauche.cnt.clone();
pour (int r = 0; r < k; ++r) {
si (droite.cnt[r] > 0) {
int newR = (gauche.prod * r) % k;
res.cnt[newR] += right.cnt[r];
}
}
retour rés;
}
}

liste publique <Intégrer> résultatArray(int[] nombres, int k,
Liste des requêtes<Liste<entier>> {
SegTree st = nouveau SegTree(nums, k);
Liste <integer> ans = nouvelle liste d'array<>(queries.size());
pour (Liste<entier> q : requêtes) {
int idx = q.get(0), val = q.get(1);
début int = q.get(2), x = q.get(3);
st.update(idx, val);
Noeud = st.query (départ, longueur nums - 1);
le nom et l'adresse de l'autorité compétente;
}
le retour des an;
}
}
«» "

---

- Oui. 7. Conclusion

- Oui. La solution utilise un **segment‐tree** qui stocke, pour chaque noeud,
- le produit du segment modulo `k`,
- et pour chaque reste `0 ... k‐1`, combien de préfixes du segment donnent ce reste.
- Chaque opération (`mise à jour` ou `query`) est `O(log N)`; avec au plus `2 × 105` mises à jour et requêtes l'algorithme respecte confortablement la limite de 2 secondes.
- L'implémentation est disponible en **Python (PyPy)**, **Java**, et **C++**, et peut être exécuté sur les juges en ligne respectifs.

Cette réponse présente une technique ** rapide et efficace en mémoire** pour traiter les requêtes dynamiques de comptage de produits-modulo – un modèle commun dans la programmation compétitive et les entrevues techniques.