---
titre: LeetCode 1293. La voie la plus courte dans une grille avec élimination des obstacles -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Chemin le plus court dans une grille avec élimination des obstacles
**(Code de bord 1293 – dur)**
*Python: Java: C++ – solution 3 langues + un billet de blog prêt à travailler*

---

Table des matières
1. [Présentation du problème](#problème-aperçu)
2. [Insights clés & Greedy](#key-insights)
3. [Conception d'algorithme] (#conception d'algorithme)
4. [Analyse de la complexité] (#analyse de la complexité)
5. [Mise en œuvre dans 3 langues] (#mise en œuvre)
* Java – visite 3-D + BFS
* Python – `collections.deque` + visite 3-D
* C++ – `struct` + `queue` + 3-D visité
6. [Le bon, le mauvais, et le mauvais]
7. [Résumé de référence et à emporter pour les intervieweurs](#seo-summary)
8. [Autres lectures et ressources](#ressources)

---

## <a name="problem-overview"></a>Présentation du problème

On vous donne une grille 2-D (`m × n`) composée de 0s (cellules libres) et 1s (obstacles).
Vous pouvez bouger ** en haut, en bas, à gauche, à droite** en un seul pas.
Vous commencez à `(0,0)` et voulez atteindre `(m‐1,n‐1)` le plus rapidement possible.

Vous êtes autorisé à détruire ** au plus `k` obstacles** (tourner un 1 en un 0).
S'il est impossible d'atteindre le but, retourner `-1`.

> **Exemples**
> 1. `grid = [[0,0,0],[1,1,0],[0,0,0],[0,1],[0,0,0]]`, `k = 1` → `6`
> 2. `grid = [[0,1],[1,1],[1,0]]`, `k = 1` → `- 1'

Contraintes (`1 ≤ m, n ≤ 40`, `1 ≤ k ≤ m × n`).

---

## <a name="key-insights"></a>Key Insights – Stratégie

Pourquoi ça compte ?
C'est-à-dire
**BFS garantit un trajet le plus court**** Parce que chaque déménagement a un coût égal (1). Autres
**L'état doit inclure les éliminations restantes**.La même cellule peut être atteinte par un chemin qui utilise moins d'éliminations, donnant plus de flexibilité plus tard. Autres
Autres **Prune états impossibles tôt** Autres
**3-D visitée array** Autres

---

## <a name="algorithm-design"></a>Algorithm Design

1. **Entrée du délai** – `État(x, y, reste_k, étapes)'.
2. **Visité** – «visité[x][y][remaining_k]» (booléen).
3. **Initialiser** – pousser `(0,0k,0)`; marquer visité.
4. **Bien que la file d'attente ne soit pas vide* *
* Pousse devant.
* Si `(x,y)` est la cible → retourner `étapes`.
* Pour chacune des 4 directions:
* Si hors des limites → sauter.
* Si la cellule suivante est un obstacle (`grid[nx][ny]==1`) et `remaining_k>0` → decrement and enqueue.
* Si la cellule suivante est libre (`grid[nx][ny]==0`) → enqueue avec la même `remaining_k`.
* Enquere seulement si cet état n'a pas encore été visité.
5. **Retour `-1`** si BFS épuise toutes les possibilités.

> **Pourquoi la visite 3-D fonctionne* *
> Pour une cellule fixe `(x,y)`, seule la matière restante *la plus élevée* est éliminée.
> Si nous atteignons la même cellule avec moins d'éliminations restantes, il ne peut pas conduire à un meilleur résultat.
> Ainsi, nous stockons le nombre exact restant; la première visite pour chaque `(x,y,remaining_k)` est optimale.

---

## <un nom="analyse de complexité"></a>analyse de complexité

Temps Espace
- Oui.
**BFS (3-D visité)**= O(m × n × (k+1)=" dans le pire des cas (chaque état traité une fois)="O(m × n × (k+1)=" pour la visite + file d'attente="

Avec `m,n ≤ 40` et `k ≤ m × n`, ceci est confortablement à l'intérieur des limites (l'état de 40 × 40 × 1600 = 2,5 M).

---

## <a name="implémentations"></a>Mise en oeuvre dans 3 langues

C'est pas vrai. Java

"Java
Importation de java.util.*;

solution de classe publique {
finale statique privée [] DIRS = {
{1, 0}, {-1, 0}, {0, 1}, {0,1}
};

public int le plus courtPath(int[][] grille, int k) {
int m = longueur de grille, n = longueur de grille[0];
Si (m) 1 & & & n == 1) retourner 0;

booléen[][][] visité = nouveau booléen[m][n][k + 1];
Queue<State> q = nouveau ArrayDeque<>();
q.offre(nouveau État(0, 0, k, 0));
visité[0][0][k] = vrai;

alors que (!q.isEmpty()) {
État cur = q.poll();
int x = cur.x, y = cur.y, restant = cur.rem, pas = cur.steps;

pour (int[]d : DIRS) {
int nx = x + d[0], ny = y + d[1];
si (nx < 0) nx >= m) ny < 0) ny >= n) continue;

int suivant Rem = restant;
Si [grid[nx][ny]] 1) {
si (rester) 0) poursuivre;
suivant De--;
}

si (nx) m - 1 && ny == n - 1) étapes de retour + 1;
si (!visité[nx][ny][nextRem]) {
visité[nx][ny][nextRem] = vrai;
q.offre(nouveau État(nx, ny, suivant les étapes + 1));
}
}
}
retour -1;
}

État de la classe statique privée {
int x, y, rem, marches;
État(int x, int y, int rem, int pas) {
This.x = x; this.y = y; this.rem = rem; this.steps = pas;
}
}
}
«» "

> **Pourquoi c'est propre** – `visited` est un 'boolean' 3-D, file d'attente stocke un `State' léger.
> Le tableau `DIRS` maintient la logique de mouvement séparée.

---

# # # # # #

'`python
à partir de collections import deque
de taper l'importation Liste

Solution de classe:
DIRS = [(1,0), (-1,0), (0,1), (0,1)]

def shortPath(self, grid: List[List[int]], k: int) -> Int:
m, n = len(grid), len(grid[0])
i m == 1 et n == 1:
retour 0

visité = [[[False] * (k+1) pour _ in range(n)] pour _ in range(m)]
q = deque([(0, 0, k, 0)]) # (x, y, reste_k, étapes)
visité[0][0][k] = Vrai

alors que q:
x, y, rem, pas = q.popleft()
pour dx, dy inself. - Oui.
nx, ny = x + dx, y + dy
si 0 <= nx < m et 0 <= ny < n:
next_rem = rem
si grille[nx][ny]] 1 :
si rem == 0:
poursuivre
suivant_rem -= 1
si nx == m-1 et ny == n-1:
étapes de retour + 1
si non visité[nx][ny][next_rem]:
visité[nx][ny][next_rem] = Vrai
q.append((nx, ny, next_rem, pas + 1))
retour -1
«» "

> **Pythonic touchs** – "deque" pour O(1) pops/pushes, compréhension de la liste pour 3-D visité.

---

C'est vrai. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

État de structure {
int x, y, rem, marches;
État(int _x, int _y, int _rem, int _steps)
: x(_x), y(_y), rem(_rem), steps(_steps) {}
};

solution de classe {
Const int DIRS[4][2] = {{1,0},{1,0},{0,1},{0,1}};
public:
int le plus courtPath(vecteur<vecteur<int>>& grille, int k) {
int m = quadrillage(), n = quadrillage[0].size();
Si (m) 1 & & & n == 1) retourner 0;

vecteur<vector<vector<bool>>> visité(
m, vecteur<vecteur<bool>>(n, vecteur<bool>(k+1, faux))
);
file d'attente <État> q;
q.emplace(0, 0, k, 0);
visité[0][0][k] = vrai;

pendant que (!q.vide()) {
État cur = q.front(); q.pop();
int x = cur.x, y = cur.y, rem = cur.rem, pas = cur.steps;

pour (auto &d : DIRS) {
int nx = x + d[0], ny = y + d[1];
si (nx < 0) nx >= m) ny < 0) ny >= n) continue;

int next_rem = rem;
Si [grid[nx][ny]] 1) {
Si (rem) 0) poursuivre;
suivant_rem--;
}

si (nx == m-1 && ny == n-1) les étapes de retour + 1;
si (!visité[nx][ny][next_rem]) {
visité[nx][ny][next_rem] = vrai;
q.emplace(nx, ny, next_rem, pas + 1);
}
}
}
retour -1;
}
};
«» "

> **C++-style** – une `structure` qui ne contient que des types primitifs, `vecteur` pour les visites 3-D, `queue` pour BFS.

---

Le bon, le mauvais et le mauvais

Ce qu'il faut éviter (Bad)
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --------------------------------------------------
**Data-Structure Choice**=3-D visité → O(1) look-ups==L'utilisation d'un ensemble de tuples* ('(x,y,rem)') dans Python ajoute un facteur de log et ralentit la mémoire. Déclarer `int[][]` en Java et oublier de se multiplier par `(k+1)` conduit à "ArrayIndexOutOfBoundsException". Autres
**Ébauche de l'état**=Cochez `if !visited[nx][ny][next_rem]=» avant de s'enquérir. Détruire un obstacle mais toujours enquêter sur le *même* `(x,y,rem)` états → boucles infinies. Autres
Autres **Début de la sortie**) Retournez immédiatement une fois que vous avez lancé la cible. Oublier de gérer le cas `1×1` bord de grille → mauvaise réponse sur petit test. Autres
Autres **Codage Style**.Conservez les directions dans une constante séparée, utilisez `struct / dataclass` pour l'état. En utilisant la récursion + mémoisation (DFS) au lieu de BFS → difficile à prouver l'optimalité. Autres

> **Ligne de bottom** – Un *correcte* BFS + 3-D visité est à la fois élégant et rapide.
> L'approche de l'équation (DFS + mémo, file d'attente prioritaire avec `k` comme priorité) peut passer de petits tests, mais échouer dans le pire des cas, et sont plus difficiles à expliquer dans une entrevue.

---

## <a name="seo-summary"></a>SEO-Ready Résumé pour les intervieweurs

- **Tenue de mots clés**: Le chemin le plus court de la grille avec élimination des obstacles – LeetCode 1293 – BFS / Java / Python / C++
- **Description détaillée**:
> Apprendre la solution LeetCode 1293 la plus dure en trois langues. Comprendre pourquoi BFS + 3-D visité est optimal, et découvrir des pièges communs qui peuvent faire ou casser votre entrevue de codage. (en milliers de dollars)
- ** Points de réflexion pour les gestionnaires d'embauche** :
* Utilisation correcte de BFS pour les trajets les plus courts
* Suivi approprié de l'état (cellules + éliminations restantes)
* Tableau visité 3-D efficace en mémoire
* Manipulation de cas de bord (1×1 grille, aucun obstacle, `k=0`)

> En présentant une solution multi-langue *polie* et en discutant des aspects bons, mauvais, laids, vous démontrez non seulement une compétence algorithmique, mais aussi ** un état d'esprit d'ingénierie logiciel** – exactement ce que les intervieweurs recherchent.

---

## <un nom="ressources"></a> Lecture et ressources supplémentaires

Thème de la ressource
C'est quoi ?
(https://leetcode.com/problèmes/shortest-path-in-a-grid-with-obstacles-elimination/discuss/) Des solutions communautaires, des astuces
Autres [Graphique BFS Basics – Big O] (https://www.geeksforgeeks.org/breath-first-search-or-bfs-for-a-graph/) BFS fondamentaux
Pourquoi nous avons besoin de la troisième dimension
(https://leetcode.com/tag/graph/) Plus de questions dures basées sur le réseau

---

### TL;DR pour votre CV / Portfolio

J'ai résolu LeetCode 1293 (Shortest Path in a Grid with Obstacles Elimination) en utilisant un BFS optimal qui suit les suppressions d'obstacles restantes dans un tableau visité en 3D. La solution fonctionne dans le temps et la mémoire `O(m·n·k)`, fonctionne en Java, Python et C++, et est une interview-favorite éprouvée.

Ajoutez ceci à votre **GitHub Gist**, **LeetCode Profile** ou **Codage-interview blog** pour montrer aux recruteurs que vous êtes prêt pour les défis de recherche graphique.

Bonne chance – et rappelez-vous : *BFS + état* est la recette de tous les problèmes de grille de chemin les plus courts ! C'est ce qu'il a dit