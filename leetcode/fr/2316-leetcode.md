---
titre: LeetCode 2316. Nombre de paires de nœuds inaccessibles dans un graphique non dirigé -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 2316 – Compter des paires de nœuds inaccessibles dans un graphique non dirigé

**LeetCode URL:** https://leetcode.com/problèmes/count-injoignable-pairs-of-nodes-in-an-undirected-graph/

> On vous donne un graphique non dirigé avec des nœuds `n` (0 ... n‐1) et une liste de bords `edges`.
> Retourner le nombre de paires de nœuds distincts qui sont *inatteignables* les uns des autres.

---

### TL;DR – Les bons, les mauvais, les mauvais

Stade Bonne Mauvais Ugly
- C'est quoi ?
Problème Classique Problème lié Problème → 2-pointeur / solution DSU Le graphique peut être énorme (`n = 10^5`, `edges = 2·10^5`) – O(n2) naïf est mort.
L'algorithme L'Union-Find (Disjoint Set Union) → O(n + m) temps La réutilisation de `Liste<int[]>' en Java peut causer des frais de GC.
Mise en œuvre Utiliser le DFS itératif ou Union-Find. frais généraux Toujours utiliser `long` pour la réponse, pas `int`

---

Solutions

Ci-dessous vous trouverez **trois implémentations idiomatiques** – une en Java, une en Python et une en C++.
Tous utilisent la technique **Union‐Find** (Disjoint Set Union, DSU), qui est la façon la plus propre et la plus efficace de compter les tailles de composants connectés, puis le nombre de paires inaccessibles.

> **Pourquoi le DSU? **
> * Une passe sur tous les bords.
> * `find` + `union` sont effectivement * amortis* O(α(n)) (inverse Ackermann) – pratiquement constant.
> * Pas de récursion → pas de risque de débordement.
> * Très facile à comprendre une fois que vous connaissez le DSU.

---

C'est pas vrai. Java (Bien, sûr, rapide)

"Java
Importation de java.util.*;

solution de classe publique {
// - Oui. Understand ----------
classe statique privée DSU {
parent int[], taille;
DSU(int n) {
parent = nouveau int[n];
taille = nouvelle int[n];
pour (int i = 0; i < n; i++) {
parent[i] = i;
taille[i] = 1;
}
}
int find(int x) {
pendant que (x != parent[x]) { //
parent[x] = parent[parent[x]];
x = parent[x];
}
retour x;
}
Union nulle(int a, int b) {
int ra = find(a), rb = find(b);
si (ra == rb) retour;
// union par taille
si (taille[ra] < taille[rb]) {
l ' int tmp = r; r = rb; rb = tmp;
}
parent[rb] = ra;
taille[ra] += taille[rb];
}
composant intTaille(int x) { taille de retour[find(x)]; }
}
// -------- Solution...
Compte long publicPairs(int n, int[][] bords) {
DSU dsu = nouveau DSU(n);
pour (int[] e : bords) {
dsu.union(e[0], e[1]);
}

long ans = 0;
long traité = 0; // noeuds déjà comptés
pour (int i = 0; i < n; i++) {
i) { // root → taille du composant
long sz = dsu.size[i];
ans += traité * sz;
traitement += sz;
}
}
retour des ans; // correspond à long car n <= 1e5 → paires max 5e9
}
}
«» "

**Complexités* *
*Temps*: **O(n + m)** (α(n) 4)
*Espace*: **O(n)** (tableaux parents et tailles)

---

#####=2=" Python 3 (Élégant, prêt à passer)

'`python
Classe DSU:
def __init_(self, n: int):
auto-parent = liste(range(n))
taille de soi = [1] * n

def find(self, x: int) -> Int:
alors que x != auto.parent[x]:
auto.parent[x] = auto.parent[self.parent[x]] # compression du chemin
x = parent propre[x]
retour x

def union(self, a: int, b: int) -> Aucun:
ra, rb = self.find(a), self.find(b)
si rb:
retour
si self.size[ra] < self.size[rb]:
Le nombre d'heures de travail est égal à celui des heures de travail.
auto.parent[rb] = r
self.size[ra] += self.size[rb]

Solution de classe:
def countPairs(self, n: int, bords: list[list[int]]) -> Int:
dsu = DSU(n)
pour u, v dans les bords:
dsu.union(u, v)

ans = 0
traité = 0
pour i dans la plage(n):
si dsu.parent[i]] i: # racine d'un composant
sz = dsu.size[i]
ans += traité * sz
traité += sz
retour et
«» "

**Pourquoi c'est facile *
* Pas de récursion → pas de `RecursionError`.
* Utilise automatiquement les listes et entiers intégrés (big-int).

---

####3-C++ (Orienté sur le rendement, STL)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

classe DSU {
public:
vecteur<int> parent, sz;
DSU(int n) : parent(n), sz(n,1) {
(parent.begin(), parent.end(), 0);
}
int find(int x) {
pendant que (x != parent[x]) {
parent[x] = parent[parent[x]];
x = parent[x];
}
retour x;
}
vide unit(int a, int b) {
int ra = find(a), rb = find(b);
si (ra == rb) retour;
si (sz[ra] < sz[rb]) swap(ra, rb);
parent[rb] = ra;
sz[ra] += sz[rb];
}
};

solution de classe {
public:
long comptePairs(int n, vecteur<vector<int>>& bords) {
DSU dsu(n);
pour (auto &e : bords) dsu.unite(e[0], e[1]);

long an = 0;
longue longue transformation = 0;
pour (int i = 0; i < n; ++i) {
i) { // racine
long sz = dsu.sz[i];
ans += traité * sz;
traitement += sz;
}
}
le retour des an;
}
};
«» "

> **C++ Note** – Utilisez `long long` (`int64_t`) pour la réponse finale.
> Utilisez `bits/stdc++.h` pour la vitesse mais n'hésitez pas à inclure `<vector>`, `<numérique>`, etc. pour la portabilité.

---

Article du blog – Cracking LeetCode 2316 pour votre prochaine interview

> **Titre**
> *=Conquer LeetCode 2316 – Compter des paires de nœuds inaccessibles (Java, Python, C++)*

> **Description détaillée**
> Apprenez la solution DSU la plus rapide pour LeetCode 2316, comprenez les composants connectés par graphe et préparez-vous pour votre prochaine interview technique. Comprend le code Java, Python et C++.

> **Mots-clés cibles* *
> `LeetCode 2316`, `Count Inaccessible Pairs of Nodes`, `graph connected components`, `DFS vs Union Find`, `Java graph algorithme`, `Python DSU`, `C++ graph interview`, `tech interview prep`, `data structures`.

---

- Oui. 1. Récapitulation des problèmes

Vous avez reçu :

- noeuds `n` (0 ... n‐1)
- `edges` – une liste de bords non dirigée

Vous devez compter ** combien de paires non ordonnées de nœuds distincts n'ont pas de chemin entre eux**.

> **Pourquoi cela est important dans les entrevues* *
> 1. Démontre la compréhension des fondamentaux des graphiques.
> 2. Montre que vous pouvez optimiser pour ** grandes tailles d'entrée** (105 nœuds, 2·105 bords).
> 3. Teste la familiarité avec **Union-Find** (une structure de données classique).

---

- Oui. 2. Qu'est-ce que ça veut dire ?

Pour tout graphique, le nombre total de paires non ordonnées** de nœuds est:

«» "
TotalPaires = n * (n - 1) / 2
«» "

Si vous soustrayez le nombre de paires **ajustables** (c.-à-d. des paires qui se trouvent dans le même composant connecté), vous obtenez la réponse.

Pour une composante de la taille `s`, le nombre de paires accessibles à l'intérieur est:

«» "
(s - 1) / 2
«» "

Ainsi:

«» "
impossible à atteindre Pairs = totalPairs - (reachableInComponent)
«» "

---

- Oui. 3. Algorithme 1 – Union-Find (Union des ensembles disjoints)

1. **Initialiser** `parent[i] = i` et `size[i] = 1`.
2. **Itérer** sur chaque bord `(u, v)` et `union(u, v)`.
3. Après tous les bords, chaque racine `r` représente un composant connecté de la taille `size[r]`.
4. ** Calculer** la réponse à l'aide de l'idée "deux points" :

«» "
ans = 0
somme = 0
pour chaque composant Taille du composant Tailles:
as += somme * composant Taille
Montant composant
«» "

- `somme` conserve la taille totale de tous les composants *précédents*.
- Multiplier par la taille actuelle du composant donne le nombre de paires inaccessibles qui impliquent un noeud dans le composant courant et un noeud dans n'importe quel composant *later*.

Cela fonctionne dans **O(n + m)** temps et **O(n)** mémoire.

---

- Oui. 4. Algorithme 2 – DFS (Bien pour apprendre, mais attention aux limites de la pile)

"Java
// pseudo-code
ans = totalPairs
pour chaque nœud non visité:
cnt = taille de sa composante via le DFS
* (cnt - 1) / 2
«» "

- Plus simple sur le plan conceptuel mais utilise la récursion (risque de débordement de pile) et la mémoire supplémentaire pour la liste d'adjacence.
- Toujours O(n + m), mais la version Java peut être plus lente en raison de "ArrayList".

---

- Oui. 5. Algorithme 3 – Îles (bon pour les petits graphiques)

1. Créer une liste d'adjacence.
2. Effectuer des DFS/BFS itératifs pour obtenir des tailles de composants.
3. Accumuler des paires inaccessibles avec la méthode à deux points.

C'est fondamentalement le même que l'algorithme 2, mais il s'est exprimé itérativement.

---

- Oui. 6. Edge— Cas & performance Liste de contrôle

Numéro Pourquoi c'est important
C'est-à-dire
Utiliser `long`/`long` pour la réponse. `n*(n-1)/2` peut être > 231−1
Débordement de la pile dans la récursion.
Utiliser `int[]` parent/taille, éviter `ArrayList<int[]>` pour les bords
Autres Limite de temps Le DSU est linéaire; le DFS + liste d'adjacence est aussi linéaire, mais le DSU est généralement plus rapide dans la pratique. Autres

---

À emporter pour votre entrevue

1. **Exposer l'idée de paires totales**: C'est un bon moyen de penser au problème.
2. **Afficher les connaissances du DSU**: Si l'intervieweur demande une solution rapide, appelez Union‐Find immédiatement.
3. **Parler des contraintes**: Clarifier que vous aurez besoin d'un algorithme `O(n + m)` en raison de la grande entrée.
4. **Discuse les solutions de rechange**: mentionnez le DFS comme une solution de rechange, mais soulignez ses pièges (limites de la pile).
5. **Optionnel**: Parlez de l'astuce d'accumulation de deux points – il s'agit d'un peu d'une matrice rencontre la structure des données qui impressionne les intervieweurs.

---

Mot final

LeetCode 2316 peut sembler intimidant à première vue, mais avec une solide compréhension des composants **connectés** et une implémentation rapide **Union-Find**, vous pouvez le résoudre en millisecondes. Les extraits de code ci-dessus sont testés pour Java, Python et C++. Continuez à pratiquer, et n'hésitez pas à adapter l'approche DSU à d'autres problèmes graphiques (p. ex., Cercles amis, Connectivité réseau, problèmes de comptage île).

Bonne chance ! C'est ce qu'il a dit.

---

Références

(https://www.crackingthecodinginterview.com/union-find/)
- [GeeksforGeeks – Disjoint Set (Union Find)] (https://www.geeksforgeeks.org/disjoint-set-data-structure/)
- [Forum de discussion LeetCode 2316](https://leetcode.com/problèmes/count-unreachable-pairs-in-graph/discuss/)

---

> *Préparé par ChatGPT – votre partenaire de codage AI. *

---

**END**