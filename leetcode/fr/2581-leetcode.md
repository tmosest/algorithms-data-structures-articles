---
titre: LeetCode 2581. Nombre de nœuds racinaires possibles -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 2581 – Nombre de nœuds racinaires possibles
Graphique / Arbre DFS / Hashing**

> **TL;DR** –
> Construire une recherche rapide pour les bords parent-enfant devinés, faire un DFS pour compter combien de devinettes sont correctes si l'arbre est enraciné au nœud 0, puis faire un second DFS qui -reroots de l'arbre. Chaque fois que nous déplaçons la racine sur un bord, nous mettons à jour le nombre de conjectures correctes dans *O(1)*. La réponse est le nombre de nœuds dont le nombre ≥ *k*.
> Complexité: **O(n + m)** temps, **O(n + m)** mémoire.

Ci-dessous vous trouverez trois implémentations prêtes à la production (Java, Python, C++) et un blog complet qui est SEO-optimisé pour les mots clés **leetcode 2581**, **tree root devine**, **DFS**, **compétitive programming**, etc.

---

Réévaluation des problèmes

Vous recevez:

Description
- C'est quoi ?
"arêtes" "n‐1" arêtes non dirigées d'un arbre (`0 ≤ noeud < n`). Autres
Chaque supposition est un bord *ordered* `[u, v]` signifiant "**u est le parent de v**. Chaque supposition est garantie pour être un bord réel de l'arbre et toutes les suppositions sont uniques. Autres
Bob affirme qu'au moins "k" de ses suppositions sont correctes pour la racine (inconnue) de l'arbre. Autres

**Retourner le nombre de nœuds qui pourraient être la racine d'un arbre qui satisfait Bob. **

---

Principales observations

1. **Root Choice est juste une réorientation de l'arbre* *
Si nous choisissons n'importe quel nœud comme racine temporaire (disons 0), nous pouvons calculer combien de devinettes sont correctes. Lorsque nous amorçons la racine à travers un bord `(p, c)` nous n'avons besoin que de mettre à jour le nombre localement:
* Si la devinette `[p, c]` est dans le jeu, elle devient **wrong** pour la nouvelle racine.
* Si la devinette `[c, p]` est dans l'ensemble, elle devient ** droite** pour la nouvelle racine.

2. **Hash Set pour la recherche rapide* *
Conservez chaque devinette comme une clé 64 bits `u * n + v` (ou une chaîne `"u#v"` dans Java/Python) afin que nous puissions interroger `O(1)` si un bord dirigé est une hypothèse.

3. **Deux transversales du DFS* *
* ** DFS1** – Root à 0, calculer le nombre initial « correct ».
* **DFS2** – Propaguer les comptes à tous les nœuds en réenracinement le long des bords, en utilisant la règle ci-dessus.
Le nombre de nœuds avec `correct >= k` est la réponse.

---

### # Code Walk‐through (Java)

"Java
Importation de java.util.*;

solution de classe {
// Encoder un bord dirigé (u, v) dans une longue clé
clé privée longue(int u, int v, int n) {
retour ((long) u) * n + v;
}

racine d'inte publiqueCount[][] bords, int[][] devines, int k) {
int n = bords.longueur + 1; // nombre de nœuds
Liste <entier>[] g = nouvelle liste de distribution[n];
pour (int i = 0; i < n; i++) g[i] = nouveau tableau <>();

// créer une liste d'adjacence
pour (int[] e : bords) {
g[e[0]].add(e[1]);
g[e[1]].add(e[0]);
}

// Ensemble de bords orientés devinés
HashSet<Long> devineSet = nouveau HashSet<>();
pour (int[] gk : devines) {
devineSet.add(key(gk[0], gk[1], n));
}

// -------- DFS1 : compter les estimations correctes lorsqu'elles sont enracinées à 0
int[] correct = nouveau int[1];
booléen[] vis = nouveau booléen[n];
dfsCount(0, -1, g, devineSet, correct, n);
base int = correcte[0]; // devine correcte pour la racine 0

// -------- DFS2 : propagation des nombres corrects à chaque noeud - Oui.
réponse int[] = nouvelle int[1];
dfsReRoot(0, -1, g, devineSet, base, k, réponse, n);
réponse de retour[0];
}

// helper DFS pour calculer le nombre correct de la base
vide privé Compte(int u, parent int,
Liste <entier>[] g,
HashSet <Long> Devinez,
int[] correct, int n) {
pour (int v : g[u]) si (v != parent) {
si (guessSet.contient(key(u, v, n))) correct[0]++; // u est parent de v
dfsCount(v, u, g, devineSet, correct, n);
}
}

// helper DFS pour re-raciner et compter les racines valides
vide privé dfsReRoot(int u, int parent,
Liste <entier>[] g,
HashSet <Long> Devinez,
Int curCorrect, int k,
réponse, int n) {
si (curCorrect >= k) réponse[0]++;

pour (int v : g[u]) si (v != parent) {
int nextCorrect = curCorrect;

// le bord (u,v) devient parent-enfant, donc:
// - si devine[u->v] était correct, nous en perdons un
si (guessSet.contient(key(u, v, n))) suivantCorrect--;

// - si devine[v->u] est correct, on en gagne une
si (guessSet.contient(key(v, u, n))) suivantCorrect++;

dfsReRoot(v, u, g, devineSet, nextCorrect, k, réponse, n);
}
}
}
«» "

> **Pourquoi c'est rapide**
> Chaque bord est visité deux fois (une fois dans chaque DFS). Toutes les recherches sont constantes parce que nous utilisons un `HashSet`.
> Mémoire: liste d'adjacence `O(n)`, devine set `O(m)`.

---

Mise en œuvre de Python

'`python
de collections importer par défautdict
de taper l'importation Liste

Solution de classe:
def rootCount(self, bords: List[List[int]],
devines : Liste[Liste[int]],
k: int) -> Int:
n = len(edges) + 1
g = defaultdict(list)
pour a, b dans les bords:
Annexe b)
g[b].appendice(a)

# encoder bord dirigé (u,v) -> chaîne "u#v"
devine_set = {"#".join(map(str, gk)) pour gk dans devine}

# DFS1 : compter les estimations correctes lorsque racine = 0
def dfs_count(u, p):
cnt = 0
pour v en g[u]:
si v == p: continuer
si f"{u}#{v}" dans devine_set:
cnt += 1
cnt += dfs_count(v, u)
retour cnt

base = dfs_count(0, -1) # devines correctes pour le noeud 0

# DFS2: reraciner et compter les nœuds valides
ans = 0
def dfs_reroot(u, p, cur):
non locaux
si cur >= k:
+= 1
pour v en g[u]:
si v == p: continuer
nxt = cur
si f"{u}#{v}" dans devine_set:
nxt -= 1
si f"{v}#{u}" dans devine_set:
nxt += 1
dfs_reroot(v, u, nxt)

dfs_reroot(0, -1, base)
retour et
«» "

> La même logique de DFS à deux passages s'applique. L'encodage de la clé utilise une simple chaîne; pour les nœuds 1 e5, une clé de chaîne est toujours confortablement rapide en CPython.

---

Mise en œuvre du C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
// Encoder le bord dirigé (u,v) comme un entier 64 bits
clé longue statique (int u, int v, int n) {
retour 1LL * u * n + v;
}

dans rootCount(vecteur<vecteur<int>>& bords,
vecteur<vecteur<int>&devines,
Int k) {
int n = bords.taille() + 1;
vecteur<vector<int>> g(n);
pour (auto &e : bords) {
g[e[0]].push_back(e[1]);
g[e[1]].push_back(e[0]);
}

_set non ordonné<long long> devine Jeu;
pour (auto & gk : devines)
devineSet.insert(key(gk[0], gk[1], n));

// ------- DFS1: base de devines correctes pour la racine 0 --------
vecteur<int> vis(n, 0);
base int = dfsCount(0, -1, g, devineSet, n);

// ------ DFS2: nombres de propagation - Oui.
Int ans = 0;
dfsReRoot(0, -1, g, devineSet, base, k, ans, n);
le retour des an;
}

particulier:
Int dfs Compte(int u, int p,
vecteur de const<vector<int>>& g,
Const unordered_set<long long>&devine Prêt,
N) {
cnt = 0;
pour (int v : g[u]) si (v != p) {
si (guessSet.count(key(u, v, n)) cnt++;
cnt += dfsCount(v, u, g, devineSet, n);
}
retour cnt;
}

vide dfsReRoot(int u, int p,
vecteur de const<vector<int>>& g,
Const unordered_set<long long>&devine Prêt,
Int curCorrect, int k,
Int& ans, int n) {
si (curCorrect >= k) ++ans;
pour (int v : g[u]) si (v != p) {
int nextCorrect = curCorrect;
si (guessSet.count(key(u, v, n))) --nextCorrect; // perdu
si (guessSet.count(key(v, u, n))) ++nextCorrect; // gagné
dfsReRoot(v, u, g, devineSet, nextCorrect, k, ans, n);
}
}
};
«» "

---

La complexité et la raison de son importance

Mesure Formule Exemple Pourquoi ça compte
-- -- -- -- -- -- -- -- -- -- -- -- -- --
**Temps**=O(n + m)==200 k opérations pour 1e5 noeuds== S'adapte confortablement sous 1 s sur LeetCode==
**Mémoire**=O(n + m)==1,5 Mo pour l'adjacence +=2 Mo pour les suppositions== Dans les limites de 256 Mo

> **Edge-Case** – Si `k == 0` la réponse est `n` (chaque noeud satisfait - au moins 0 devines correctes).
> **Edge-Case** – Si `gueses` est vide, la réponse est `n` aussi.

---

Article de blog (SEO-Ready)

> **Titre**: Code Leet 2581 – Nombre de nombre de nœuds racinaires possibles Solution DFS
> **Meta-description**: Solve LeetCode 2581 (hard) avec une solution propre O(N) DFS en Java, Python et C++. Apprenez comment reraciner un arbre, utilisez le hachage pour deviner la recherche, et compter les racines valides dans le temps linéaire.

---

C'est vrai. 1. Présentation

LeetCodes 2581 -Count Nombre de possibles nœuds racinaires est un problème d'arbre classique qui voyage souvent vers les débutants parce qu'il mélange **arêtes non dirigées** avec **devinées ordonnées**. La clé d'une solution rapide est un DFS à deux passages qui *reracine* l'arbre. Dans cet article, vous allez voir:

* Problème reformulé pour plus de clarté
* Une implémentation complète et prête à la production en **Java**, **Python** et **C++**
* Une preuve étape par étape de l'exactitude
* Analyse de complexité
* Les pièges communs et les
* Cas d'essai d'échantillons

Si vous êtes un programmeur compétitif, un recruteur ou simplement un fan de LeetCode, les idées ici vont augmenter votre vitesse de codage et votre performance d'entrevue.

---

C'est vrai. 2. Aperçu du problème

Compte tenu d'un arbre de nœuds `n`, `m` devines ordonnées `[u, v]` (=u est parent de v=), et d'un entier `k`, nous devons compter combien de nœuds pourraient être la racine de telle sorte qu'au moins `k` devines soient correctes.

Principales contraintes :

Valeur des contraintes
C'est pas vrai.
Jusqu'à 100k nœuds
Jusqu'à 100 k de conjectures
< 0 ≤ k ≤ m > Seuil

Tous les bords sont uniques, l'arbre est connecté, et chaque supposition est un véritable bord dirigé de l'arbre.

---

C'est vrai. 3. Intuition

1. **Root est un Point de vue** – Correction d'un nœud comme racine temporaire (disons node 0). L'arbre devient un arbre dirigé.
2. **Le compte de la correction est local** – Lorsque nous déplaçons la racine de parent `p` à enfant `c` le long du bord `(p,c)` seulement deux bords dirigés changent d'état:
* `[p,c]` perd la justesse
* `[c,p]` peut gagner la justesse
3. **Hash Set for Constant‐Time Query** – Stockez toutes les conjectures dans un ensemble de bords orientés.
4. **Deux DFS** –
* **DFS‐Base**: Compter les estimations correctes pour la racine arbitraire.
* **DFS-Reroot**: Marchez à nouveau dans l'arbre, mettez à jour le nombre local et comptez les nœuds dont le nombre ≥ `k`.

---

C'est vrai. 4. Algorithme

«» "
1. Construire une liste d'adjacence de l'arbre.
2. Entreposez toutes les conjectures dirigées dans un jeu de hachage (u * n + v) // Clé 64 bits
3. DFS1 : racine au nœud 0
- Pour chaque enfant v de u, si devine[u->v] dans l'ensemble -> ++correct
- accumuler récursivement des hypothèses correctes
-> correct[0] = nombre de base correct pour la racine 0
4. DFS2: reraciner l'arbre
- Commencez au nœud 0 avec curCorrect = base
- Pour chaque bord (u,v) (u parent, v enfant)
nextCorrect = curCorrect
si devine[u->v] -> SuivantCorrect...
si devine[v->u] -> suivantCorrect++
- Récurser en enfant v avec nextCorrect
- Chaque fois que curCorrect ≥ k, incrémenter la réponse
5. Réponse de retour
«» "

**Proof d'exactitude* *

*Lemme 1* – Dans un arbre enraciné, une supposition «[u,v]» est correct **iff** `u` est le parent de `v`.
*Proof*: conséquence directe de la définition. *

*Lemme 2* – Lorsque nous déplaçons la racine de `p` à son enfant `c`, le nombre de suppositions correctes ne change que d'au plus 1 pour chacune des deux bordures dirigées `(p,c)` et `(c,p)`.
*Profit*:
- La supposition `[p,c]` (si présent) était correcte lorsque `p` était parent; après reracinement `c` devient parent, donc il devient faux → diminuer de 1.
- L'hypothèse "[c,p]" (si présent) devient correcte → augmentation de 1.
Aucun autre changement de statut. *

*Theorem* – Après DFS2, pour chaque nœud `x` la variable `curCorrect` est égale au nombre de devinettes qui seraient correctes si `x` était la racine.
*Proof*: par induction au-dessus de DFS2. Cas de base : la racine 0 satisfait déjà le théorème. Étape inductive: supposons que le théorème tient pour parent `p`. Pour enfant `c` nous calculons `nextCorrect` exactement comme Lemma 2 décrit, d'où le théorème tient pour `c`. *

Parce que l'algorithme compte tous les nœuds avec `curCorrect ≥ k`, la réponse finale est correcte.

---

C'est vrai. 5. Analyse de la complexité

Étape Temps Espace
C'est pas vrai.
Construire une liste d'adjacence Autres
Construisez le jeu de devinettes Autres
Découpe de récursions de l'O(n)
Empilement de récursion DFS2
**Total**

Les deux passes sont linéaires, de sorte que la solution fonctionne confortablement sous les limites de temps de LeetCode typiques.

---

C'est vrai. 6. Faits saillants de la mise en œuvre

*Java*
- Utilise la touche `longe` (`1L * u * n + v`) pour éviter les collisions.
- `ArrayList<int[]>` pour l'adjacence; `HashSet<Long>` pour les hypothèses.
- Deux méthodes d'aide `dfsCount` et `dfsReRoot`.

*Python*
- Utilise des touches de chaîne comme `"u#v"` ou 64-bit entier; les deux sont assez rapides.
- DFS récursif avec "sys.setrecursionlimit".

*C++*
- Utilise `unordered_set<long>` pour les requêtes O(1).
- fonction `key(u,v,n)` pour calculer la clé 64-bit.

---

C'est vrai. 6. Pièges communs

1. **Encodage de clé Wong** – Utilisation `u*10^5 + v` peut déborder 32-bit. Utilisez 64 bits («long long»).
2. **Dépassement de stock** – Python recursion profondeur par défaut 1000; augmenter avec `sys.setrecursionlimit(200000)`.
3. **Empty Guess Set** – Si `m=0`, la réponse est `n`. Poignez tôt si vous le souhaitez.
4. **k == 0** – Tous les nœuds satisfont au seuil; pas besoin d'exécuter DFS2 (optimiser si vous voulez).

---

C'est vrai. 6. Essais d ' échantillon

'`python
♪ Essai 1: k=0 (trivial)
affirme countPossibleRootNodes(n=4, m=0, k=0) == 4

♪ Essai 2: Chaîne simple
# Arbre: 1-2-3
♪ Devine : [1,2], [2,3]
* k=1 -> Seulement root 1 fonctionne
affirme countPossibleRootNodes(3, 2, 1, [(1,2),(2,3)]) 1

# Test 3: Arbre de l'étoile
# 1 connecté à tous les autres
♪ Devinez (1,2),(1,3),(1,4),(2,1),(3,1),(4,1)
* k=3 -> tous les nœuds satisfont
affirme countPossibleRootNodes(5, 6, 3, ...) 5
«» "

---

C'est vrai. 7. A emporter

L'astuce de reracinement DFS à deux passages est un modèle puissant pour les problèmes qui impliquent le comptage des propriétés directionnelles sur les arbres (p. ex., tailles de sous-arbres, profondeur maximale, somme des profondeurs, etc.). Combinez-le avec un jeu de hachage pour les requêtes à temps constant, et vous aurez une solution O(N) qui passe même les contraintes les plus serrées.

Bon codage, et bonne chance sur LeetCode 2581!

---

C'est vrai. 8. Références et lectures supplémentaires

* [Technique de reracinement des arbres](https://cp-algorithms.com/graph/tree_dfs.html#reracinement)
* [LeetCode Discussions – 2581] (https://leetcode.com/problems/count-number-of-possible-root-nodes/discuss/)
* [Programme concurrentiel 3 – Section des arbres] (https://cpbook.readthedocs.io/en/latest/trees.html)

---

> **Auteur**: *Votre nom*, programmeur et passionné de LeetCode. Suivez-moi sur Twitter @YourHandle pour plus de pierres précieuses algorithmiques.