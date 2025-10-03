---
titre: LeetCode 317. Distance la plus courte de tous les bâtiments -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 317. Distance la plus courte de tous les bâtiments
**Stratégie SFB + multi-sources* *

> **TL;DR** – Pour chaque bâtiment exécute un BFS pour accumuler la distance à chaque cellule vide, gardez un compteur d'accès pour savoir quand une cellule peut voir tous les bâtiments, et finalement prendre la distance minimale accumulée.

---

Code

Voici les solutions **ready‐to‐paste** dans **Java, Python et C++** qui compilent avec les compilateurs standards (Java 17, Python 3.10+, C++17).
Tous les trois utilisent le même algorithme : pour chaque bâtiment exécuter un BFS, ajouter la distance à chaque terrain vide accessible, compter combien de bâtiments chaque terrain vide peut atteindre, et finalement choisir la cellule vide qui peut atteindre *tous* bâtiments avec la plus petite somme.

---

##### Java 17

"Java
Importation de java.util.*;

solution de classe publique {
DX = {0, 1, 0, -1};
int final statique privé[] DY = {1, 0, -1, 0};

public Distance(int[][] grille) {
i (grid) = null=" grid.longueur == 0) retour -1;
int m = longueur de grille, n = longueur de grille[0];

int[][] dist = nouvelle int[m][n]; // distance accumulée
int[][] atteindre = nouveau int[m][n]; // combien de bâtiments peuvent atteindre cette cellule
Bâtiment int. Nombre = 0;

pour (int i = 0; i < m; i++) {
pour (int j = 0; j < n; j++) {
si [grid[i][j]] 1) { // un bâtiment
bâtiment Nombre++;
bfs(grid, i, j, dist, harnais, m, n);
}
}
}

réponse int = entier. MAX_VALEUR;
pour (int i = 0; i < m; i++)
pour (int j = 0; j < n; j++)
si [grid[i][j]] 0 && reach[i][j] == buildingCount)
réponse = Math.min(réponse, dist[i][j]);

réponse de retour == Integer. MAX_VALEUR ? -1 : réponse;
}

vide privé bfs[int[]] grille, int sx, int sy,
int[]] dist, int[][] atteindre,
m, n) {
booléen[][] visité = nouveau booléen[m][n];
Queue<int[]> q = nouveau ArrayDeque<>();
q.offre(nouvelle int[]{sx, sy});
visité[sx][sy] = vrai;
niveau int = 0; // distance du bâtiment

alors que (!q.isEmpty()) {
taille int = q.size();
pour (int i = 0; i < taille; i++) {
[] cur = q.poll();
pour (int d = 0; d < 4; d++) {
Int nx = cur[0] + DX[d];
int ny = cur[1] + DY[d];
si (nx < 0) nx >= m) ny < 0) ny >= n) continue;
si (grid[nx][ny] != 0== visite[nx][ny]) continue;
visité[nx][ny] = vrai;
Dist[nx][ny] += niveau + 1;
[nx][ny]++;
q.offre(nouvelle int[]{nx, ny});
}
}
niveau++;
}
}

// Harnais d'essai rapide
public statique vide principal(String[] args) {
int[[]] grille1 = {
[1, 0, 2, 0, 1],
[0, 0, 0, 0],
{0, 0, 1, 0, 0}
};
Système.out.println(nouvelle solution().shortestDistance(grid1)); // 7

int[] [] quadrillage2 = {{1,0}};
System.out.println(nouvelle solution().shortestDistance(grid2)); // 1

int[] [] quadrillage3 = {{1}};
System.out.println(nouvelle solution().shortestDistance(grid3)); // -1
}
}
«» "

---

#### Python 3.10+

'`python
à partir de collections import deque
de taper l'importation Liste

Solution de classe:
def le plus court Distance(auto, grille: Liste[Liste[int]]) -> Int:
si ce n'est pas une grille[0]:
retour -1

m, n = len(grid), len(grid[0])
dist = [[0] * n pour _ dans l'intervalle(m)] # distance accumulée
= [[0] * n pour _ dans l'intervalle(m)] # combien de bâtiments peuvent atteindre
constructions = somme (compte de ligne(1) pour la ligne de la grille)

À droite, en bas, à gauche, en haut
dirs = [(0, 1), (1, 0), (0, -1), (-1, 0)]

pour i dans la plage (m):
pour j dans la plage(n):
si grille[i][j]] 1: # commencer BFS de chaque bâtiment
visité = [[Faux] * n pour _ dans l'intervalle(m)]
q = deque([i, j, 0)]) # (x, y, distance)
visité[i][j] = Vrai

alors que q:
x, y, d = q.popleft()
pour dx, dy en dirs:
nx, ny = x + dx, y + dy
si 0 <= nx < m et 0 <= ny < n \
0 et non visité[nx]:
visité[nx][ny] = Vrai
dist[nx][ny] += d + 1
à atteindre[nx][ny] += 1
q. appendice((nx, ny, d + 1))

meilleure = flotteur('inf')
pour i dans la plage (m):
pour j dans la plage(n):
si grille[i][j]] 0 et atteindre[i][j]== bâtiments:
best = min(best, dist[i][j])

retour -1 si meilleur == flotter('inf') sinon meilleur


♪ Démo
si __nom__ == "__main__" :
sol = Solution()
print(sol.shortestDistance([[1, 0, 2, 0, 1], [0, 0, 0, 0], [0, 0, 1, 0]) # 7
print(sol.shortestDistance([[1, 0]])) # 1
print(sol.shortestDistance([[1]]) Numéro 1
«» "

---

C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
dans la plus courte Distance(vecteur<vecteur<int>>& grille) {
si (grid.vide()=" grid[0].vide() retourne -1;
int m = quadrillage(), n = quadrillage[0].size();

vecteur<vector<int>> dist(m, vector<int>(n, 0));
vecteur<vector<int>> atteindre(m, vecteur<int>(n, 0));
Bâtiment int. Cnt = 0;

const int dx[4] = {0, 1, 0, -1};
const int dy[4] = {1, 0, -1, 0};

pour (int i = 0; i < m; ++i)
pour (int j = 0; j < n; ++j)
si [grid[i][j]] 1) {
+ construction Cnt;
bfs(grid, i, j, dist, portée, dx, dy, m, n);
}

int ans = INT_MAX;
pour (int i = 0; i < m; ++i)
pour (int j = 0; j < n; ++j)
si [grid[i][j]] 0 && atteindre[i][j] == construireCnt)
as = min(ans, dist[i][j];

INT_MAX ? -1 : ans;
}

particulier:
vide bfs(vector<vector<int>>& grille, int sx, int sy,
vectorielle<vector<int>>& dist, vectorielle<vector<int>>& atteindre,
m, int n) {
vector<vector<bool>> visité(m, vector<bool>(n, false));
file d'attente <tuple<int,int,int>> q; // x, y, distance
q.emplace(sx, sy, 0);
visité[sx][sy] = vrai;

pendant que (!q.vide()) {
auto [x, y, d] = q.front(); q.pop();
pour (int dir = 0; dir < 4; ++ dir) {
int nx = x + dx[dir];
int ny = y + dy[dir];
si (nx < 0) nx >= m) ny < 0) ny >= n) continue;
si (grid[nx][ny] != 0== visite[nx][ny]) continue;
visité[nx][ny] = vrai;
dist[nx][ny] += d + 1;
à atteindre[nx][ny] += 1;
q. mettre en place(nx, ny, d + 1);
}
}
}
};

// Démo
Int main() {
Solution sol;
vecteur<vecteur<int>> g1 = {{1,0,2,0,1},
{0,00,00,0},
{0,1,0,0}};
cout << sol.shortestDistance(g1) << endl; // 7

vecteur<vecteur<int>> g2 = {{1,0}};
cout << sol.shortestDistance(g2) << endl; // 1

vecteur<vector<int>> g3 = {{1}};
cout << sol.shortestDistance(g3) << endl; // -1
}
«» "

---

Aperçu algorithmique

C'est vrai. 1. Pourquoi BFS de chaque bâtiment?

- BFS garantit la distance *la plus courte* à chaque cellule vide accessible car elle s'étend uniformément couche par couche.
- Pour un bâtiment à `(sx, sy)`, la première couche (distance 1) est ses voisins immédiats, la seconde couche (distance 2) est l'anneau suivant, etc.
- Ajouter `(level + 1)` au tableau `dist` donne la bonne distance Manhattan.

C'est vrai. 2. Distance accumulée + compteur d'accès

- "dist[x][y]" stocke la somme **** des distances entre *tous* bâtiments pouvant atteindre `(x, y)`.
- "Atteinte[x]" compte combien de bâtiments ont atteint `(x, y)`.
Seules les cellules avec la réponse totale sont valides.

C'est vrai. 3. Complexité

- Que `B` soit le nombre de bâtiments, `M × N` la taille de la grille.
Chaque BFS visite chaque cellule vide au plus une fois: `O(M·N)` par bâtiment.
**Temps total**: "O(B · M · N)".
Dans le pire des cas (chaque cellule est un bâtiment à l'exception d'une cellule vide), "B ≤ M·N", donc "O(M·N)^2)" – encore d'amende pour les contraintes ('M, N ≤ 50').

- **Mémorie**: trois matrices entières/booléennes `M × N` → `O(M·N)`.

C'est vrai. 4. Cas de bord

- Oui. Aucune terre vide accessible → répondre `-1`.
- Toutes les cellules sont des bâtiments ou des obstacles → `-1`.
- Grille avec des cellules `0` qui peuvent atteindre *certains* mais pas *tous* bâtiments sont automatiquement jetés par le compteur de portée.

---

- Oui. La bonne, la mauvaise, la mauvaise de la solution

**Beau**
C'est pas vrai.
Simplicité : un BFS par bâtiment, aucune structure de données compliquée. Facteur constant potentiellement élevé : une file d'attente par bâtiment. Aucun – le BFS est propre et déterministe. Autres
**Readability**
**Performance** Même que Java. Autres
**Mémoire** $ 3 × M × N int + 1 × M × N bool $ 4 × 502 $ 10 kB.
**Scalabilité**= Fonctionne jusqu'à 200 × 200 (mais LeetCode max est 50). Même chose.

---

- Oui. Comment utiliser dans les entrevues

1. ** Expliquez l'idée** d'abord : Pour chaque bâtiment, lancez un BFS et accumulez des distances. (en milliers de dollars)
2. **Afficher une langue** (souvent Java ou Python) et *hand-write* la logique de base.
3. **Discuse la complexité** et pourquoi l'algorithme est optimal pour les contraintes.
4. **Répondez à une question astucieuse**: Que faire si la grille n'a pas de 0-cellable pour tous les bâtiments? → répondre `-1`.

---

### Questions courantes sur ce problème

Question Conseil
- C'est quoi ?
*Qu'en est-il si `M` et `N` sont 1000? *= Besoin de réduire le nombre de traverses BFS; peut-être un BFS multi-sources de tous les bâtiments à la fois. Autres
Autres *Vous trouvez la réponse dans l'heure O(M·N)?* Impossible dans le pire des cas parce que vous devez connaître les distances à chaque bâtiment. Autres
*Et si les obstacles sont dynamiques?*=Relancer BFS à partir de cellules modifiées ou maintenir des mises à jour progressives. Autres
Autres *Paralléliser les BFSes?*=Le BFS de chaque bâtiment est indépendant – peut utiliser des fils, mais attention aux mises à jour `dist`/`reach` partagées. Autres
*Pourquoi BFS et pas DFS? * , DFS ne garantit pas des chemins plus courts dans une grille non pondérée. Autres

---

- Oui. Quoi faire?

- **Accumuler** et **compte** en un seul passage par bâtiment.
- **Réutiliser** la même distance et atteindre les matrices sur tous les BFS.
- **Vérifier** l'état de tous les bâtiments avant de prendre la minute.
- **Time/Space** sont tous les deux O(M·N) par bâtiment – amende pour le LeetCode 50×50 limite.

---

Prochaines étapes

1. Pratiquez ce modèle sur des problèmes similaires de LeetCode:
* 317 – *Distance la plus courte de tous les bâtiments* (même problème).
* 1472 – *Horaires de trains optimaux* (BFS basé sur le réseau).
* 317 – *Distance la plus courte de tous les bâtiments* (version Java).
2. Essayez de *optimiser* pour les grandes grilles en utilisant **BFS** multisource ou **préfixer des sommes**.

---

- Oui. La bonne, la mauvaise, la mauvaise de la solution

**Beau**
C'est pas vrai.
**Readability** Grande plaque de chaudière (p. ex. matrice visitée par BFS). Aucun.
**Performance**= Excellent pour les contraintes; chaque BFS touche chaque cellule vide une seule fois. Un peu de frais généraux par bâtiment : créer une nouvelle matrice "visitée".
**Tableaux de mémoire**=O(M·N)=; négligeable pour les limites de LeetCode. Même chose.
Fonctionne sur Java 17+ sans changement. Autres

---

La pensée finale

**LeetCode="Shortest Distance from All Buildings="** est un exemple de manuel de **BFS** multi-source dans une grille.
Un seul passage sur la grille (compte des bâtiments) + un BFS par bâtiment (accumulant les distances et les nombres d'accès) donne la réponse optimale.
Maîtrisez ce modèle, et vous cracherez de nombreuses questions d'entrevue basées sur la grille, et vous serez prêt à impressionner avec un code propre et multilingue lors de votre prochaine entrevue. C'est ce qu'il a dit.

Bon codage !