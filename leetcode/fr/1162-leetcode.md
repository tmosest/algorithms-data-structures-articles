---
titre: LeetCode 1162. Aussi loin de la terre que possible -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## C'est aussi loin que possible de la terre – LeetCode 1162
**Moyenne de l'espace O(n2)

> **Objectif** – Pour une grille carrée `n × n` de `0`s (eau) et `1`s (terre), trouver une cellule d'eau dont la distance Manhattan jusqu'à la cellule terrestre *nearest* est **maximisée**.
> Retourner cette distance maximale ou `-1` si la grille ne contient que du sol ou seulement de l'eau.

---

Pourquoi ce problème se pose pour les entrevues

C'est bien, c'est mal.
C'est pas vrai.
**Intuitive** – Le système multi-sources est un ajustement naturel. **Continué** – Les grilles de terre/d'eau vides ou les grilles de toutes les terres/d'eau nécessitent une manipulation spéciale. Autres
**Réutilisable** – Le même modèle BFS résout de nombreux problèmes de distance à la cible la plus proche. ** Limites de temps** – Pour `n = 100`, le BFS touche 10 000 cellules, ce qui est bien, mais la récursion naïve (DFS) peut faire sauter la pile. **Mutable input** – Certaines solutions modifient la grille d'entrée pour économiser de l'espace, mais cela est généralement découragé lors des entrevues. Autres

---

Déclaration de problème (paraphrasée)

> **Input**: `int[[]] grid`, `n = grid.length` (`n == grid[i].length`), `grid[i][j] < = {0, 1}`.
> **Output**: `int` – la plus grande distance de Manhattan entre n'importe quelle cellule d'eau et sa cellule terrestre la plus proche, ou `-1` si aucune cellule d'eau de ce type n'existe.

> **La distance manhattane** entre `(x0, y0)` et `(x1, y1)` est `=x0−x1=" +=0−y1=".

---

## ☐ Intuition et stratégie de haut niveau

1. **BFS multisources**
* Traiter chaque cellule terrestre `(i, j)` comme un nœud source. *
*Enseignez d'abord toutes les cellules terrestres. *
2. **Agrandissement par couche* *
*Quand nous pop une cellule, nous explorons ses quatre voisins. *
*Si un voisin est de l'eau (`0`), il est découvert à distance `current_distance + 1`. *
3. **Tirer la distance maximale**
*Chaque fois que nous terminons l'exploration d'une couche BFS entière, nous incrémentons le compteur de distance. *
*Le compteur après le dernier calque est la réponse. *

S'il n'y a pas de cellules terrestres (`queue vide`) ou que chaque cellule est une terre (`queue size == n2`), nous retournons `-1`.

---

Détails de la mise en œuvre

Mots clés Autres
C'est pas vrai.
Utiliser `Queue<int[]>` ou `ArrayDeque`. Gardez un `boolean[][] visité` ou modifiez la grille. Autres
**Python** pour la file d'attente. Utiliser la compréhension de la liste pour les directions. Autres
**C++**"queue<pair<int,int>". Utilisez un vecteur 2-D pour `visited` ou modifiez `grid`. Autres

Nous fournirons *clean*, *commenté* code pour chaque langue.

---

Code – Java

"Java
Importation de java.util.*;

***
* LeetCode 1162: Aussi loin de la terre que possible
* BFS – multisources (toutes les cellules terrestres)
*/
solution de classe publique {
intérieur public maxDistance(int[][] grille) {
int n = longueur de la grille;
Queue<int[]> q = nouveau ArrayDeque<>();
booléen[][] visité = nouveau booléen[n];

// 1/ Réduisez toutes les cellules terrestres dans la file d'attente
pour (int i = 0; i < n; i++) {
pour (int j = 0; j < n; j++) {
si [grid[i][j]] 1) {
q.offre(nouvelle int[]{i, j});
visité[i][j] = vrai; // marque telle que visitée
}
}
}

// / / / / / /
si (q.isEmpty()="q.size()="n * n) retourne -1;

int[] dx = {1, -1, 0, 0};
int[] dy = {0, 0, 1, -1};
distance int = -1; // deviendra 0 après la première couche

BFS standard
alors que (!q.isEmpty()) {
int sz = q.size();
distance++; // nous déplaçons un autre calque
pour (int k = 0; k < sz; k++) {
[] cur = q.poll();
pour (int dir = 0; dir < 4; dir++) {
Int ni = cur[0] + dx[dir];
int nj = cur[1] + dy[dir];
si (ni < 0) ni >= n) continuer;
si (visité[ni][nj]) se poursuit;
visité[ni][nj] = vrai;
q.offre(nouvelle int[]{ni, nj});
}
}
}
distance de retour;
}
}
«» "

---

Code – Python

'`python
à partir de collections import deque
de taper l'importation Liste

Solution de classe:
def maxDistance(self, grille: List[List[int]]) -> Int:
n = len(grid)
q = deque()

# 1-
pour i dans la plage(n):
pour j dans la plage(n):
si grille[i][j]] 1 :
q. appendice(i, j))

Pas de terre ou pas d'eau
si non q ou len(q) == n * n:
retour -1

dirs = [(1,0), (-1,0), (0,1), (0,-1)]
dist = -1

N° 3
alors que q:
dist += 1
pour _ dans la plage(len(q)):
x, y = q.popleft()
pour dx, dy en dirs:
nx, ny = x + dx, y + dy
si 0 <= nx < n et 0 <= ny < n et grille[nx]]] 0:
quadrillage[nx][ny] = 1 # marque visitée par conversion en terre
q. appendice((nx, ny))

retour
«» "

> **Pourquoi nous mutons "grid"?**
> Dans Python il est commun de muter l'entrée pour éviter un tableau extra visité.
> Dans les entretiens, être explicite si la mutation est autorisée; sinon, créer une matrice "visitée".

---

Code – C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int maxDistance(vecteur<vecteur<int>>& grille) {
int n = quadrillage.size();
file d'attente <pair<int,int>> q;
vector<vector<bool>> visité(n, vector<bool>(n,false));

Toutes les cellules terrestres
pour (int i=0;i<n;i++){
pour (int j=0;j<n;j++){
si (grid[i][j]==1){
q.emplace(i,j);
visité[i][j]=vrai;
}
}
}

si (q.vide()=" (int)q.size() == n*n) retourne -1;

dirs[4][2] = {1,0},{1,0},{0,1},{0,1},{0,1}};
dist = -1;

BFS
pendant que [!q.vide()]{
int sz = q.size();
dist++; // incrément de la couche
pour (int k=0;k<sz;k++){
auto [x,y] = q.front(); q.pop();
pour (auto &d: dirs){
int nx = x + d[0], ny = y + d[1];
si (nx <0.
si (visité[nx][ny]) continue;
visité[nx][ny] = vrai;
q.emplacer(nx,ny);
}
}
}
de retour;
}
};
«» "

---

Analyse de complexité

Mesure Raison
C'est pas vrai.
Chaque cellule est enquêtée/traitée au plus une fois → `O(n2)` Autres
**Space**=Quue + tableau visité → `O(n2)` Autres

> **Pourquoi `O(n2)` est optimal* *
> La réponse peut être aussi grande que `2n-2` (par exemple, tout terrain sur un coin).
> Tout algorithme qui lit l'ensemble de la grille doit toucher chaque cellule → liée à la ligne inférieure `ш(n2)`.

---

Pièges communs

Piège
- Oui.
**Récursif DFS** – débordement de la pile sur les grandes grilles
**Cas de bord manquants** – tous les `0`s ou tous `1`s=Cochez explicitement la taille de la queue avant BFS=
**Mise à jour de la grille en place** – peut violer les contraintes d'entretien.
** Compteur de distance de Wong** – commençant par `-1` vs `0`= Initialiser `dist = -1` et incrément *après* traitement d'une couche

---

Variations et extensions

Les changements
C'est quoi ?
** Grille pondérée** – chaque cellule a un coût.
Remplacer `1` par n'importe quelle valeur cible
**K‐th terrain le plus proche**

---

Liste de contrôle prête à être déployée

1. **Choisissez BFS** – toujours le choix sûr pour les problèmes de distance jusqu'à la fin de la cible.
2. **Handle all-land / all-water tôt** – cela évite beaucoup de confusion.
3. ** Clarifier les règles de mutation** – si l'entrevue est stricte sur l'immutabilité d'entrée.
4. **Commentairenez votre code** – montrez que vous comprenez ce que chaque bloc fait.
5. **Réduire l'échantillon* *

"Java
int[[]] grille = {{1,0,0},
{0,00,0},
{0,1}};
System.out.println(nouvelle solution().maxDistance(grid)); // 2
«» "

---

Comment faire pour avoir l'entrevue

1. ** Expliquez l'idée BFS d'abord** – il montre que vous connaissez le bon paradigme algorithmique.
2. **Parcourir les cas de bord** – démontrer que vous connaissez les conditions `-1`.
3. **Ecrivez un code clair et tapé** – utilisez une file d'attente de gabarit, un tableau de directions et un compteur.
4. **Discuss alternatives** – Je pourrais aussi muter la grille pour sauver la mémoire, mais je vais la garder pure ici. (en milliers de dollars)

---

LT;DR

- Utiliser **BFS** multi-sources – demander toutes les cellules terrestres.
- Étendre la couche par la couche, incrémenter un compteur "distance".
- Retourner le compteur après la dernière couche (ou `-1` pour les cas de bord).

> C'est tout ce qu'il y a pour être loin de Land, simple, élégant et prêt à l'interview!

Bon codage, et que vos réponses soient toujours **le plus loin possible**