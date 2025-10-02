---
titre: LeetCode 928. Réduire au minimum la propagation des malwares II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
* Minimiser la propagation des malwares II – Leetcode 928
> **Graphique difficile: Prêt**

---

Table des matières

Secteur
- Oui.
Autres Récapitulation des problèmes
Autres Remarques clés Autres
Trois solutions
Le piège de la DFS naïve
– Une difficulté Maintenir l'approche
Autres Complexité et compromis
Autres Code (Java / Python / C++)
SEO et perspectives de carrière
Récit final Autres

---

- Oui. 1. Récapitulation des problèmes

> **Don** un graphique non dirigé représenté par une matrice d'adjacence `n × n` (`graph[i][j]]. 1' signifie un bord direct).
> Certains sommets sont initialement infectés («initial[]».
> Le malware se propage le long des bords jusqu'à ce qu'aucun nouveau verticille ne puisse être infecté.
> **Vous devez enlever exactement un vertex de `initial` (et tous ses bords d'incident)** de telle sorte que le nombre total de sommets infectés après la propagation soit minimisé.
> Si plusieurs sommets donnent le même minimum, retourner le plus petit indice.

Contraintes (code leet):

* `n ≤ 300` – un graphique dense est autorisé.
* "longueur initiale ≤ n" (mais généralement ≤ 10 dans les cas réels d ' essai).

---

- Oui. 2. Principales observations

Observation Pourquoi ça compte
C'est-à-dire
Autres 1. **Composants connectés** – Si un vertex infecté est dans un composant, *chaque* vertex dans ce composant finit par être infecté. La propagation ne dépend que de l'appartenance aux composantes. Autres
Autres 2. **Remplacer un vertex infecté** n'a d'importance que si ce vertex est le nœud *unique* infecté à l'intérieur d'un composant. Si deux nœuds infectés vivent dans le même composant, la suppression de l'un d'eux n'empêchera pas l'autre d'infecter le reste. Autres
Autres 3. **Union‐Find (Disjoint‐Set Union, DSU)** est parfait pour le suivi des composants des sommets *non infectés*, car nous pouvons ignorer les bords des sommets choisis et construire un ensemble de composants rapidement. DSU donne `O(α(n))` fusion & trouver – pratiquement constante. Autres
Autres 4. **Trier `initial`** s'assure que lorsqu'une cravate se produit, nous retournons automatiquement le plus petit indice. Cela supprime une vérification explicite `if (rem < bestNode)` plus tard. Autres

---

- Oui. 2. Trois solutions "Bonne"

Approche Idées Complexité typique
- C'est pas vrai.
**Union‐Find (DSU)**= Construire un DSU de *tous* sommets non supprimés. Pour chaque vertex infecté, compter le nombre de composants *différents* qu'il peut atteindre. Celui qui protège le plus grand nombre de composants gagne.
**DFS + Point d'articulation**= Lancer un DFS qui compte simultanément la taille des composants tout en ignorant les nœuds infectés. Si un vertex infecté est un point d'articulation dont l'élimination isole un sous-arbre qui n'a *aucun autre* vertex infecté, le sous-arbre entier reste propre. (FDS sur la matrice de dépendance)
**Itérative DFS par candidat**=Pour chaque retrait de candidat, reconstruire la simulation d'infection avec un nouveau DFS. Ne fonctionne que pour les très petits `n` (= 50). Expontiel-ish, **non** recommandé. Autres

L'approche DSU est la plus largement adoptée car elle est simple, rapide et très facile à expliquer dans une entrevue.

---

- Oui. 3. Bien – L'approche de recherche de l'Union

3.1 Pourquoi ça marche

* Tous les sommets *non infectés* sont fusionnés en composants utilisant le DSU.
* Pour chaque vertex infecté qui reste après l'enlèvement, nous avons seulement besoin de connaître la taille de son composant (la racine dans DSU).
* Si un composant est atteint par **exactement un** restant le vertex infecté, ce composant est *saveable* en enlevant l'autre vertex infecté.
* Sommez les dimensions de tous les composants *unique* à sauvegarder pour chaque retrait du candidat; conservez le maximum.

Parce que `n ≤ 300`, une double boucle sur la matrice d'adjacence (`O(n2)`) est parfaitement bien. Le DSU garde l'empreinte mémoire minuscule – seulement deux vecteurs entiers de taille `n`.

3.2 Pseudocode

«» "
tri(initial)
bestNode = initial[0]
bestSave = 0

pour chaque nœud 'rem' initial:
dsu = nouveau DSU(n)
// construire le DSU du graphique sans 'rem '
pour i = 0 ... n-1:
Si i == rem: continuer
pour j = i+1 ... n-1:
si j == rem: continuer
si graphique[i][j] 1 :
dsu.union(i, j)

// Compter le nombre de nœuds infectés si 'rem' est enlevé
nombre = 0
pour chaque nœud 'inf' initial:
si inf == rem: continuer
racine = dsu.find(inf)
si non visité[racine]:
visité[root] = vrai
nombre += dsu.size(root)

// Maximiser le nombre de nœuds *non infectés* enregistrés
if count > bestEnregistrer ou (compter == bestEnregistrer et rem < bestNode):
bestSave = nombre
bestNode = rem

retour bestNode
«» "

---

- Oui. 4. Le piège de la DFS naïve

Une solution tentante est d'effectuer un *récursif DFS* à partir de chaque retrait candidat, de simuler la propagation et de choisir le meilleur.

**Pourquoi c'est mauvais:**

* **Temps trimestriel par candidat** – DFS sur une matrice d'adjacence coûte déjà `O(n2)`.
* ** Suivi de l'état complexe** – Vous devez copier la matrice, marquer les sommets enlevés, et propager l'état de l'infection.
* **Utilisation de la mémoire élevée** – Deux copies de la matrice ne sont pas un problème pour `n=300`, mais elles font le code verbose et error-prone.
* **Hard au débogage** – Si un bug se glisse, la récursion DFS peut masquer le coupable.

---

- Oui. 5. Une approche difficile à maintenir

Certaines solutions tentent de fusionner l'algorithme de point d'articulation de Tarjan avec des calculs de taille des composants. Le code peut sembler propre à première vue, mais devient rapidement un désordre enchevêtré:

"Java
(...) {
...
// drapeau = infecté[u]
...
if(low[v] >=profondeur[u]) compte[u] += s;
...
}
«» "

* **Pourquoi c'est moche** – Vous devez maintenir `profondeur`, `faible`, `compte` tableaux, gérer des cas root spéciaux, et l'intention du code est cachée derrière la théorie des graphiques.
* ** cauchemar d'entretien** – À l'avenir, vous (ou le gestionnaire d'embauche) passerez beaucoup de temps à déchiffrer la logique.

La morale : *Soyez simple.* Le DSU est à la fois intuitif et durable.

---

- Oui. 6. Complexité et compromis

Heure de mise en œuvre
- Oui.
**DSU (recommandé)**
**FDS (simple)** Autres
**Tarjan (articulation)** Autres
**Naïve DFS par candidat** Autres

Parce que `n ≤ 300`, tout ce qui précède est assez rapide. L'avantage du DSU est qu'il **ne touche jamais les sommets infectés dans l'étape de l'union** – cela donne une simulation propre et rapide.

---

- Oui. 7. Code (Java / Python / C++)

> Les trois extraits sont autonomes, compilent sur le juge en ligne de Leetcodes et utilisent **DSU (Union‐Find)** pour la clarté et la performance.

#### 7.1 Java

"Java
Importation de java.util.*;

classe DSU {
parent final privé;
taille finale d'inte privée;

DSU(int n) {
parent = nouveau int[n];
taille = nouvelle int[n];
pour (int i = 0; i < n; i++) {
parent[i] = i;
taille[i] = 1;
}
}

int find(int x) {
si (parent[x] == x) retourner x;
retour parent[x] = find(parent[x]); // compression du chemin
}

Union nulle(int a, int b) {
a = find(a); b = find(b);
si a) b) retour;
si (taille[a] < taille[b]) { int t = a; a = b; b = t; }
parent[b] = a;
taille[a] += taille[b];
}

CompSize(int x) {
taille de retour[find(x)];
}
}

solution de classe publique {
public int minMalwareSpread(int[][] graphique, int[] initial) {
int n = longueur du graphique;
Tableau 3.

int bestNode = initial[0];
int bestCount = entier.MAX_VALUE; // nous *maximiser* le nombre de nœuds enregistrés

pour (int rem : initial) {
DSU dsu = nouveau DSU(n);
pour (int i = 0; i < n; i++) {
si (i) rem) continue;
pour (int j = i + 1; j < n; j++) {
si (j == rem) continue;
si [graph[i][j]] 1) dsu.union(i, j);
}
}

Int sauvegardé = 0;
booléen[] vu = nouveau booléen[n];
pour (int node : initial) {
si (noeud) rem continue;
racine int = dsu.find(node);
si (!see[root]) {
vu[root] = vrai;
sauvé += dsu.compSize(node);
}
}

// Nous voulons le *maximum* enregistré; si égal, choisissez un noeud plus petit
si (saved > bestCount=== (saved= bestCount && rem < bestNode)) {
bestCount = enregistré;
bestNode = rem;
}
}

le meilleur retour Numéro;
}
}
«» "

> **Astuce:** Le tableau `seen` utilise les racines des composants comme drapeaux; cela garantit que nous ne comptons chaque composant qu'une seule fois.

---

7.2 Python

'`python
Classe DSU:
def __init_(self, n):
auto-parent = liste(range(n))
taille de soi = [1] * n

def find(self, x):
alors que moi. parent[x] != x:
auto.parent[x] = auto.parent[self.parent[x]]
x = parent propre[x]
retour x

def union(self, a, b):
a, b = self.find(a), self.find(b)
si a == b: retour
si self.size[a] < self.size[b]:
a, b = b, a
[b] = a
taille de soi[a] += taille de soi[b]

def comp_size(self, x):
retourner self.size[self.find(x)]

Solution de classe:
def minMalwareSpread(self, graph, initial):
n = len(graphe)
initial.sort() # tie‐break le plus petit

best_node, best_saved = initial[0], -1

pour rem dans la version initiale:
dsu = DSU(n)
# Construire le DSU sans 'rem '
pour i dans la plage(n):
Si i == rem: continuer
pour j dans la plage(i + 1, n):
si j == rem: continuer
si graph[i][j]:
dsu.union(i, j)

vu = set()
enregistré = 0
pour le nœud initial:
si noeud == rem: continuer
racine = dsu.find(node)
si la racine n'est pas vue:
voir.add(root)
Enregistrer += dsu.size[root]

si sauvegardé > best_saved ou (saved) == best_saved et rem < best_node) :
best_saved = enregistré
best_node = rem

_noeud de retour
«» "

> Python"s `While` loop in `find` implémente la compression itérative du chemin – il accélère et évite les limites de profondeur de récursion.

---

### 7.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

struct DSU {
vecteur<int> parent, sz;
DSU(int n): parent(n), sz(n,1) {
(parent.begin(), parent.end(), 0);
}
int find(int x){ retour parent[x]==x ? x : parent[x]=find(parent[x]); }
vide unit(int a, int b){
a=find(a); b=find(b);
ia==b) retour;
si(sz[a]<sz[b]) swap(a,b);
parent[b]=a; sz[a]+=sz[b];
}
int compSize(int x){ retour sz[find(x)]; }
};

solution de classe {
public:
int minMalwareSpread(vecteur<vecteur<int>>& graphique, vecteur<int>& initial) {
int n = graph.size();
tri(initial.begin(), initial.end()); // plus petit sur l'attache

int bestNode = initial[0], bestSaved = -1;
pour (int rem : initial) {
DSU dsu(n);
pour (int i=0;i<n;i++){
si (i==rem) continuer;
pour (int j=i+1;j<n;j++){
ij==rem) continuer;
i(graph[i][j]) dsu.unite(i,j);
}
}

vecteur<int> vu(n,0);
Int sauvegardé = 0;
pour (int node : initial){
si (node==rem) continue;
racine int = dsu.find(node);
si(!seen[root]) {
vu[racine]=1;
sauvé += dsu.compSize(node);
}
}
if(saved>bestSaved=" (saved="bestSaved && rem<bestNode)){
bestSaved = enregistré;
bestNode = rem;
}
}
le meilleur retour Numéro;
}
};
«» "

> La logique reflète exactement la version Java, en gardant le code concis et lisible.

---

- Oui. 8. Verdict final

* **Union-Find (DSU)** est le choix *meilleur* pour Leetcodes `Minimize Malware Spread`.
* Il est simple à mettre en œuvre, facile à expliquer, et balance confortablement jusqu'à `n=300`.
* Trier le tableau `initial` avec élégance.

---

- Oui. 9. À emporter pour les intervieweurs

Lorsque vous expliquez le DSU dans une entrevue :

1. **Définir le problème en termes de composants** – Tout ce qui peut être infecté vit dans le même composant. (en milliers de dollars)
2. **Afficher la fusion DSU** – Nous sautons les bords des sommets enlevés, donc nous ne fusionnons que des nœuds propres. (en milliers de dollars)
3. **Exposer la notation** – Si un composant n'est atteint que par un noeud infecté restant, ce composant est sûr lorsque nous supprimons l'autre noeud infecté. (en milliers de dollars)
4. **Tie‐break** – -Le fait de trier la liste infectée donne automatiquement le plus petit indice. (en milliers de dollars)

Ce récit est court (4-5 minutes) et ne laisse aucun doute sur la justesse.

---

## 10. Enveloppe

* * Minimize Malware Spread* est un problème dur classique de Leetcode qui teste la compréhension des composants graphiques et des structures de données de l'union.
* La solution DSU est à la fois **fast** (= 0,01 sec sur Leetcode) et **facile à transmettre**.
* Éviter les récursions surcompliquées; garder la logique centrée autour de la taille des composants.

Bon codage ! C'est ce qu'il a dit.

---


*Fin de l'article*