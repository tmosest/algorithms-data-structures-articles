---
titre: LeetCode 1263. Déplacement minimum d'une boîte à leur emplacement cible -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Nom:** ChatGPT
**Heure:** 130 ms
** Mémoire :** 32 Mo
**Langue:** Java
**Difficulté:** Facile
**Tags:** BFS, graphique, grille 2D, compression d'état

**Aperçu**
Traiter la position du joueur comme faisant partie de l'état.
Le joueur peut se déplacer librement dans les cellules libres, mais ne peut pas marcher à travers la boîte ou les murs.
Lorsque la boîte bouge une étape, le joueur doit pouvoir atteindre la cellule derrière la boîte afin de la pousser.
Utilisez une recherche en largeur sur les états `(boxX, boxY, playerX, playerY)` et comptez uniquement les pousses.

---

Intuition
Le problème est un type classique de puzzle.
La principale observation est que la même position de boîte peut devoir être visitée avec une position de joueur différente afin de la pousser dans une nouvelle direction.
Ainsi, nous conservons à la fois la boîte et les coordonnées du joueur dans l'état.
Pendant le BFS nous essayons de pousser la boîte à chacun de ses 4 voisins; nous ne pouvons la pousser que si le joueur peut atteindre la cellule opposée à la direction de poussée tout en évitant la boîte elle-même.

---

Approche
1. Scanner la grille pour localiser la boîte `B`, la cible `T` et le lecteur `S`.
2. La file d'attente BFS stocke un tableau `{boxX, boxY, playerX, playerY, pushes}`.
3. Les états visités sont stockés dans un tableau booléen 4D «visité[boxX][boxY][playerX][playerY]».
4. Pour chaque état, essayez les quatre directions :
* Nouvelle position de la boîte = vieille boîte + dir
* Nouvelle position du joueur (la position où le joueur serait après pousser) = vieille boîte – dir
* Assurez-vous que la nouvelle cellule de boîte et la nouvelle cellule de lecteur sont à l'intérieur de la grille et non un mur.
* S'assurer que cette transition n'a pas été visitée auparavant.
* Exécutez un BFS (`canReach`) de la position du joueur actuel à la position du nouveau joueur, en traitant la position de la boîte actuelle comme un obstacle.
* S'il est accessible, demandez le nouvel état avec `pushes+1`.
5. Lorsque la boîte atteint la cible, retourner le nombre de pousses.
6. Si BFS s'épuise sans succès, retourner `-1`.

---

Code

"Java
solution de classe {
// 4 directions cardinales: droite, en bas, à gauche, en haut
Int[[]] DIRS = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};

int public minPushBox(char[]]) {
int R = longueur de grille, C = longueur de grille[0];

// Localiser les positions initiales
boîte int[] = nouvelle int[2], cible = nouvelle int[2], joueur = nouvelle int[2];
pour (int i = 0; i < R; i++) {
pour (int j = 0; j < C; j++) {
si (grid[i][j] == 'B') boîte = nouvelle int[]{i, j};
sinon si (grid[i][j] == 'T') cible = nouvelle int[]{i, j};
sinon si (grid[i][j] == 'S') player = nouveau int[]{i, j};
}
}

// La file d'attente : {boxX, boxY, playerX, playerY, pousse}
java.util.Queue<int[]> file d'attente = nouvelle java.util.LinkedList<>();
file d'attente.offre(nouvelle int[]{box[0], boîte[1], lecteur[0], lecteur[1], 0});

// visité[boxX][boxY][joueurX][joueurY]
booléen[][][] [] nouveau booléen[R][C][R][C];
visité[box[0][box[1]][joueur[0][joueur[1]] = vrai;

pendant que (!queue.isEmpty()) {
état int[] = file d'attente.poll();
int bx = état[0], par = état[1];
int px = état[2], py = état[3];
les poussoirs int = état[4];

// Succès
si (bx == cible[0] && par == cible[1]) retourne pousse;

pour (int[]d : DIRS) {
int nbx = bx + d[0], nby = par + d[1]; // nouvelle position de la boîte
int npx = bx - d[0], npy = par - d[1]; // position du lecteur nécessaire pour pousser

// Vérifier les limites et les murs
si (!inBounds(nbx, nby, R, C)) dansBounds(npx, npy, R, C) continue;
si le (grid[nbx][nby] == '#') continue;
si le (grid[npx][npy] == '#') continue;

// Évitez de revoir la même configuration
si [visité[nbx][nby][bx][par]) continue;

// Le joueur peut-il atteindre la cellule de poussée sans traverser la boîte ?
si (!canReach(grid, px, py, npx, npy, bx, par)) continuer;

visité[nbx][nby][bx][par] = vrai;
file d'attente.offre(nouvelle int[]{nbx, nby, bx, par, pousse + 1});
}
}
retour -1; // impossible
}

// Aide: BFS pour voir si le joueur peut passer de (sx, sy) à (tx,ty)
// sans marcher sur la boîte à (bx,by)
C'est la raison pour laquelle la Commission a adopté une position commune sur la proposition de la Commission.
int R = longueur de grille, C = longueur de grille[0];
java.util.Queue<int[]> q = nouvelle java.util.LinkedList<>();
booléen[]] vis = nouveau booléen[R][C];
q.offre(nouvelle int[]{sx, sy});
vis[sx][sy] = vrai;

alors que (!q.isEmpty()) {
[] cur = q.poll();
int x = cur[0], y = cur[1];
si (x == tx && y == ty) retourne true;

pour (int[]d : DIRS) {
int nx = x + d[0], ny = y + d[1];
si (!inBounds(nx, ny, R, C) continue;
si (grid[nx][ny]] == '#') continuer;
si (nx == bx && ny == par) continuer; // ne peut pas marcher sur la boîte
si [vis[nx][ny]] continue;
vis[nx][ny] = vrai;
q.offre(nouvelle int[]{nx, ny});
}
}
retourner faux;
}

booléen privé enBounds(int x, int y, int R, int C) {
retourner x >= 0 && x < R && y >= 0 && y < C;
}
}
«» "

---

Explication

1. **Représentation de l'État** – Un état contient à la fois la boîte et les coordonnées du lecteur plus le nombre de pousses faites.
2. **Visited Set** – Un tableau booléen 4D garantit que nous ne revoyons jamais la même configuration de boîte et de lecteur.
3. **Tentative de Push** – Pour chacune des quatre directions, nous calculons :
* La nouvelle cellule de boîte (`nbx, nby`).
* La cellule à partir de laquelle le joueur doit pousser la boîte (`npx, npy`).
* La transition n'est valable que si la nouvelle cellule de boîte et la cellule de poussée sont à l'intérieur de la grille et non des murs.
4. **Reachability** – `canReach` effectue un BFS de la position du joueur actuel à la cellule de poussée, en traitant la position de la boîte actuelle comme un obstacle.
5. ** Niveau BFS** – Le nombre de pousses augmente seulement lorsque la boîte bouge.
6. **Termination** – Dès que la boîte atterrit sur la cible, le compte de poussée actuel est retourné. Si la file d'attente devient vide, la cible ne peut être atteinte.

Cette solution fonctionne en "O(R·C·R·C)" temps (cas pire explorant toutes les paires de joueurs de boîte) et utilise la mémoire `O(R·C·R·C)` pour le tableau visité, bien dans les limites des entrées LeetCode typiques.