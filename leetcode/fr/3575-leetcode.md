---
titre: LeetCode 3575. Note maximale du sous-arbre -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Score maximal du sous-arbre – un arbre-DP avec des bitmasks* *
*Java-friendly blog post

---

- Oui. 1. Récapitulation des problèmes

On nous donne un arbre non dirigé enraciné au nœud **0**.
Chaque nœud `i` a une valeur `vals[i]` (1 ≤ `vals[i]` ≤ 109).
Un sous-ensemble de nœuds à l'intérieur d'un sous-arbre est appelé **bon** si, lorsque vous écrivez toutes les valeurs sélectionnées en décimale, **chaque chiffre 0–9 apparaît au plus une fois**.
(Si une valeur contient un chiffre répété – par exemple 121 – elle ne peut jamais appartenir à un bon sous-ensemble.)

Pour chaque noeud `u` nous avons besoin de la somme maximale d'un sous-ensemble de bonne qui se trouve entièrement dans le sous-arbre de `u`.
Enfin nous revenons

«» "
(somme sur tous les nœuds de ce maximum) mod 1 000 000 007
«» "

«par[i]» décrit l'arbre:
`par[0] = -1` et pour chaque `i>0` il y a un bord `(par[i] , i)`.

«n = longueur égale ≤ 500».

La tâche consiste à calculer efficacement la réponse.



---

- Oui. 2. Idée de haut niveau

1. **Masque Digit** – Pour une valeur `x` nous construisons un masque 10 bits.
* bit `d` est 1 chiffre `d` se produit dans `x`.
* Si un chiffre apparaît deux fois, le masque est *invalide* (retourner `-1`).

2. **DP sur masques** –
Pour un sous-arbre, nous conservons un tableau `dp[1024]` où

«» "
dp[mask] = somme maximale qui n'utilise que les chiffres définis dans 'mask '
«» "

(Si `mask` est un sous-ensemble des chiffres déjà utilisés, la somme correspondante peut être atteinte.)

3. **Ajouter un nœud** –
Supposons que le nœud actuel ait un masque `S` (valable).
Nous pouvons étendre chaque ensemble précédemment réalisable `M` qui est **disjoint** avec `S`.
C'est-à-dire pour chaque sous-masque `m` de `~S` que nous faisons

«» "
dp[m= S] = max(dp[m= S], dp[m] + vals[node])
«» "

4. ** Petite à grande fusion** –
La fusion naïve de deux tables DP pour enfants nécessiterait une convolution sur des masques *disjoints* (310 à 59 000 ops par fusion).
Avec **petit à grand** nous gardons le PDD du plus grand enfant et le reste des enfants un noeud à la fois.
Chaque nœud est reprogrammé au plus `O(log n)`, ce qui donne un coût total `O(n log n · 210)` qui est trivial pour `n ≤ 500`.

---

- Oui. 2. Le PDD in-depth

Symbole Signification
C'est quoi ?
`mask`=10-bit entier – les bits de set représentent les chiffres utilisés
`dp[mask]`=" meilleure somme qui utilise exactement les chiffres de `mask`="
"S"" masque de la valeur actuelle du nœud (ou `-1` s'il contient un chiffre répété)
"ALL = 1023" (binaire 1111111111)

Ajouter un nœud avec le masque `S`

Texte
pour chaque sous-masque «m» de (ALL ^ S) // masques qui n'utilisent PAS de chiffres de S
dp[m= S] = max( dp[m= S] , dp[m] + val )
«» "

L'énumération des sous-masques utilise l'astuce classique "pour (int m = sub; m; m = (m-1) & sub)", qui coûte au plus 1024 itérations par noeud.

- Oui. Résultat pour un sous-arbre

Une fois que tous les enfants ont été fusionnés et que le nœud actuel a été ajouté, la réponse pour le sous-arbre est simplement «dp[ALL]» – la meilleure somme qui peut utiliser **toute** série de chiffres.

---

- Oui. 3. Petite à grande technique

1. **DFS** – Traverser les listes d'adjacence de construction d'arbres de `par`.
2. Pour chaque nœud «u»:
* Calculer de façon récursive les tables DP de tous les enfants.
* Choisissez l'enfant avec le plus grand sous-arbre (`bigChild`) et *réutiliser* son tableau DP comme base (`dp`).
* Ajouter le noeud `u` à `dp`.
* Pour chaque *autre* enfant `v` (les "small" ou "small") dirige un assistant `addSubtree(v, dp)` qui marche à travers tout le petit sous-arbre et ajoute chaque noeud au même `dp`.
C'est sûr parce que nous sommes seulement **appending** nœuds, ne fusionnant jamais deux tableaux DP complets.

Le nombre de fois où un noeud est réinséré est égal au nombre d'ancêtres qui l'ont choisi comme enfant *petit*, qui est limité par `O(log n)`.

---

- Oui. 4. Croquis d'exactitude

* **Le masque Digit** garantit qu'aucune valeur avec des chiffres répétés ne contribue jamais à un bon sous-ensemble.
* La règle de mise à jour DP combine uniquement des ensembles de chiffres qui sont *disjoint*, de sorte que le sous-ensemble résultant reste bon.
* Le sous-ensemble vide est implicitement représenté par les zéros initiaux dans le tableau DP.
* La réponse pour chaque noeud est `dp[ALL]`, qui est le maximum sur tous les masques, c'est-à-dire la somme maximale de tout sous-ensemble de bien à l'intérieur de ce sous-arbre.

---

- Oui. 5. Analyse de la complexité

Étape Temps Espace
C'est pas vrai.
Liste des bâtiments proches de l'immeuble Autres
DFS + petits-à-grands (en milliers de dollars)

Java et C++ ont besoin de 64 bits ("long long" / "long") pour les sommes intermédiaires; la réponse finale est prise modulo 1 000 000 007.

---

- Oui. 6. Cas et notes de bord

Traitement des dossiers
C'est pas vrai.
Valeur = 0: Non autorisé par les contraintes, mais "getMask" le traite comme un seul chiffre 0.
Autres Tous les nœuds sont invalides. Autres
Autres Arbre en forme d'étoile.Le petit à grand retraitement de chaque feuille n'est qu'une fois → encore rapide. Autres

---

- Oui. 7. Mise en œuvre du code

Voici des solutions propres, prêtes à copier et à coller pour **Java 17**, **Python 3.10** et **C++17**.
Tous les trois suivent la même logique que celle décrite.

---

#### 7.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
int final statique privé MOD = 1_000_000_007;
int final statique privé FULL_MASK = (1 << 10) - 1; // 1023

public int goodSubtreeSum(int[] vals, int[] par) {
int n = par. longueur;
Liste <entier>[] g = nouvelle liste de distribution[n];
pour (int i = 0; i < n; ++i) g[i] = nouvelle liste de distribution<>();

pour (int i = 1; i < n; ++i) g[par[i]].add(i);

long[] ans = nouveau long[n];
int[] sz = nouvelle int[n];
dfs(0, vals, g, ans, sz);

somme longue = 0;
pour (long v : ans) somme += v;
retour (int) (somme % MOD);
}

/** profondeur-première recherche – retourne le tableau dp pour le sous-arbre enraciné à u */
long[] dfs(int u, int[] vals, Liste<entier>[] g,
long[] ans, int[] sz) {
sz[u] = 1;
long[] dp = nul; // tiendra le DP de l'enfant le plus lourd
int heavy = -1;

pour (int v : g[u]) {
longue[] enfant = dfs(v, vals, g, ans, sz);
sz[u] += sz[v];
si (lourd) {
lourd = v;
dp = enfant; // réutiliser le DP de l'enfant lourd
}
}

si (dp == null) dp = nouveau long[FULL_MASK + 1];

addNode(u, vals, dp);

// Fusionner les petits enfants en les ajoutant au nœud
pour (int v : g[u]) {
si (v != heavy) addSubtree(v, vals, g, dp);
}

ans[u] = dp[FULL_MASK]; // meilleur sur tous les masques
retour dp;
}

/** ajouter tous les nœuds du sous-arbre enracinés à u dans un tableau dp existant */
vide privé addSubtree(int u, int[] vals, List<integer>[] g, long[] dp) {
addNode(u, vals, dp);
pour (int v: g[u]) ajouterSubtree(v, vals, g, dp);
}

/** ajouter un seul noeud au tableau dp */
vide privé addNode(int u, int[] vals, long[] dp) {
masque int = digitMask(vals[u]);
si (masque < 0) retour; // valeur a un chiffre → répété ne peut pas être utilisé

int free = masque FULL_MASK ^; // masques qui n'utilisent PAS les chiffres de ce nœud
// itérer sur tous les sous-masques de 'free' en ordre décroissant
pour (int sub = free; sub > 0; sub = (sub - 1) & free) {
int newMask = masque sous-jacent;
dp[newMask] = Math.max(dp[newMask], dp[sub] + vals[u]);
}
dp[mask] = Math.max(dp[mask], vals[u]); // cas où nous prenons seulement ce noeud
}

/** retourne bitmask de chiffres ou -1 si un chiffre se répète dans x */
chiffre int privé Masque(int x) {
Int vu = 0;
pendant que (x > 0) {
Int d = x % 10;
si ((see & (1 << d))) != 0) retour -1;
vu= (1 << d);
x/= 10;
}
retour vu;
}
}
«» "

---

7.2 Python

'`python
de taper l'importation Liste

MOD = 1 000 000 007
FULL = (1 << 10) - 1 # 1023

Solution de classe:
Bien SubtreeSum(self, vals: List[int], par: List[int]) -> Int:
n = len(par)
g = [[] pour _ dans l ' intervalle n)]
pour i dans la plage (1, n):
g[par[i]].appendice(i)

ans = [0] * n
sz = [0] * n
Auto.dfs(0, vals, g, ans, sz)

Total = somme(s) % MOD
retour total

def dfs(self, u: int, vals: List[int], g: List[List[int]],
ans: Liste[int], sz: Liste[int] -> Liste[int]:
sz[u] = 1
dp = Aucune
lourd = -1

pour v en g[u]:
enfant = auto.dfs(v, vals, g, ans, sz)
sz[u] += sz[v]
-1 ou sz[v] > sz[lourd]:
lourd = v
dp = enfant

si dp n'est pas:
dp = [0] * (FULL + 1)

auto.add_node(u, vals, dp)

pour v en g[u]:
Si v != lourd:
Self.add_subtree(v, vals, g, dp)

ans[u] = dp[FULL] # meilleur sur tous les masques
retour dp

def add_subtree(self, u: int, vals: List[int], g: List[List[int]], dp: List[int]):
auto.add_node(u, vals, dp)
pour v en g[u]:
Self.add_subtree(v, vals, g, dp)

def add_node(self, u: int, vals: List[int], dp: List[int]):
masque = auto.digit_mask(vals[u])
si masque < 0: # chiffre répété – ne peut pas faire partie d'un bon sous-ensemble
retour
libre = masque FULL ^
sub = libre
tandis que sous:
Nouveau = masque sous-=
dp[new] = max(dp[new], dp[sub] + valeurs[u])
sous = (sous - 1) & libre
dp[masque] = max(dp[masque], vals[u])

def digit_mask(self, x: int) -> Int:
vu = 0
alors que x:
d = x % 10
si vu & (1 << d):
retour -1
vu= 1 << d
x //= 10
retour vu
«» "

---

### 7.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int bonne Sous-arbreSum(vecteur<int>& vals, vecteur<int>&par) {
MOD = 1'000'000'007;
int n = par.size();
vecteur<vector<int>> g(n);
pour (int i = 1; i < n; ++i) g[par[i]].push_back(i);

vecteur <long> meilleur(n);
vecteur <int> sz(n);
dfs(0, vals, g, best, sz);

somme longue = 0;
pour (auto v : meilleur) somme += v;
retour int(somme % MOD);
}

particulier:
= (1 << 10) - 1; // 1023

vecteur<long long> dfs(int u, vecteur<int>& vals,
vecteur<vecteur<int>>& g,
vecteur<long long>&meilleur, vecteur<int>&sz) {
sz[u] = 1;
vectorielle <long long> dp; // sera réglé sur le DP d'enfant lourd
int heavy = -1;

pour (int v : g[u]) {
enfant automatique = dfs(v, vals, g, best, sz);
sz[u] += sz[v];
si (lourd) {
lourd = v;
dp = std: move(enfant);
}
}

si (dp.vide()) dp.assign(FULL + 1, 0);

addNode(u, vals, dp);

pour (int v : g[u]) si (v != heavy) addSubtree(v, vals, g, dp);

best[u] = dp[FULL];
retour dp;
}

vide addSubtree(int u, vector<int>& vals,
vecteur<vecteur<int>>& g,
vecteur <long>&dp) {
addNode(u, vals, dp);
pour (int v: g[u]) ajouterSubtree(v, vals, g, dp);
}

vide addNode(int u, vector<int>& vals, vector<long long>& dp) {
masque int = digitMask(vals[u]);
si (masque < 0) retour; // chiffre répété – sauter

int free = masque FULL ^;
pour (int sub = free; sub; sub = (sub - 1) & free) {
int newMask = masque sous-jacent;
dp[newMask] = max(dp[newMask], dp[sub] + vals[u]);
}
dp[mask] = max(dp[mask], (long)vals[u];
}

Digit intMask(int x) {
Int vu = 0;
pendant que x) {
Int d = x % 10;
si (voir & (1 << d)) retour -1;
vu= 1 << d;
x/= 10;
}
retour vu;
}
};
«» "

---

- Oui. 8. Résumé et à emporter

* **Les masques Digit + DP sur les masques** donnent une façon élégante d'appliquer la règle .
* **Petit à grand** maintient la solution rapidement même sur des arbres denses.
* L'algorithme fonctionne confortablement dans les limites de `n ≤ 500` tout en étant facile à comprendre et à mettre en œuvre.

N'hésitez pas à copier l'extrait de code dans votre soumission de LeetCode ou à l'utiliser comme exemple d'enseignement pour les arbres + bitmask + petits modèles à grands.



---



---

** Bon codage !**