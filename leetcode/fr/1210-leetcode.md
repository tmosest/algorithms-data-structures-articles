---
titre: LeetCode 1210. Mouvements minimums pour atteindre la cible avec rotations -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 1210 – **Le minimum se déplace pour atteindre la cible avec des rotations* *
*Le bon, le mauvais, et le laid – comment le casser en Java, Python & C++ *

---

- Oui. 1. Récapitulation des problèmes

«» "
Entrée : int[][] grille // 0 = vide, 1 = bloqué
Sortie: nombre minimum de mouvements, ou -1 si impossible
«» "

Le serpent est toujours deux cellules longues:

Cellules occupées
C'est-à-dire
(r, c) et (r, c+1)
(r, c) et (r+1, c)

* État de départ : **Horizontal** au coin supérieur gauche → cellules (0,0) et (0,1).
* État cible : **Horizontal** au coin inférieur droit → cellules (n‐1, n‐2) et (n‐1, n‐1).
* Un mouvement peut être :

État Résultat
C'est quoi ?
Les deux cellules peuvent se déplacer à droite
Les deux cellules peuvent changer d'orientation
Le sens de l'horloge et les deux cellules ci-dessous sont vides
Dans le sens contraire des aiguilles d'une montre, les deux cellules verticales à droite sont vides.

`n` est au plus 100, donc un BFS exhaustif sur tous les états est possible.



---

- Oui. 2. Pourquoi la première recherche (BFS)

* Chaque état (position + orientation) a un coût fixe de 1 pour atteindre l'état suivant.
* BFS garantit que la première fois que nous pop l'état cible de la file d'attente, nous avons utilisé le nombre minimum de mouvements.
* L'espace d'état est limité: `n × n × 2 ≤ 20 000` – trivial pour le matériel moderne.



---

- Oui. 3. Idée de base de la BFS (en anglais)

1. **Représenter un état** comme `(ligne, col, orientation)` où `row, col` sont les coordonnées de la cellule *head* (la cellule supérieure ou la plus gauche).
2. Gardez un tableau booléen 3D «visité[n][n][2]» pour éviter de revoir les états.
3. Commencez par `(0, 0, 0)` – horizontale.
4. Alors que la file d'attente n'est pas vide :
* Pop a state, incrément `steps`.
* Si c'est la cible, retournez les "étapes".
* Générer jusqu'à quatre nouveaux états en appliquant les quatre règles de déplacement; ajouter ceux qui sont légaux et non visités à la file d'attente.
5. Si la file d'attente se vide sans frapper la cible → retourner `-1`.



---

- Oui. 4. Liste de contrôle des cas de bord

Autres Vérification Pourquoi c'est important
- Oui.
Se déplaçant à droite pendant **horizontal** – doit vérifier la cellule `(r, c+2)` est à l'intérieur de la grille et vide. Autres
Se déplaçant à droite pendant **vertical** – doit vérifier que `(r, c+1)` et `(r+1, c+1)` sont vides. Autres
Autres Rotation dans le sens des aiguilles d'une montre – besoin **deux** cellules sous le serpent pour être vides: `(r+1, c)` et `(r+1, c+1)`. Autres
En tournant dans le sens contraire des aiguilles d'une montre, il faut que **les deux** cellules à la droite du serpent soient vides: `(r, c+1)` et `(r+1, c+1)`. Autres
Autres Ne jamais sortir de la grille (`r < 0`, `c < 0`, `r+1 >= n`, `c+1 >= n`). Autres
Autres La cible elle-même doit être sur des cellules vides – le problème le garantit, mais les contrôles défensifs aident à éviter les bogues cachés. Autres

---

- Oui. 5. Mise en œuvre

Ci-dessous sont propres, implémentations idiomatiques dans **Java, Python, et C++**.
Tous les trois suivent le même schéma BFS décrit ci-dessus.

#### 5.1 Java 17

"Java
Importation de java.util.*;

***
* LeetCode 1210 – Déplacements minimum pour atteindre la cible avec rotations
*/
solution de classe publique {
interne statique privée HORIZ = 0, VERT = 1;
intérieur statique final int[] DR = {0, 0}; // à droite, en bas pour horizontale
intérieur statique final int[] DC = {1, 1};

Int minimum public Déplace(int[][] grille) {
int n = longueur de la grille;
booléen[][][] visité = nouveau booléen[n][n][2];
Queue<State> q = nouveau ArrayDeque<>();

// début: horizontale à (0,0)
visité[0][0][HORIZ] = vrai;
q.offre(nouveau État(0, 0, HORIZ));

Étapes int = 0;
la cibleR = n - 1, la cibleC = n - 2;

alors que (!q.isEmpty()) {
int sz = q.size();
pendant la période (sz-- > 0) {
État cur = q.poll();
int r = cur.r, c = cur.c, ori = cur.ori;

si (r) la cible Objectif C && ori == HORIZ) les étapes de retour;

// ---- 1. Déplacer à droite
si (peut déplacer la droite(grid, r, c, ori)) {
État nxt = nextRight(r, c, ori);
si (!visité[nxt.r][nxt.c][nxt.ori]) {
visité[nxt.r][nxt.c][nxt.ori] = vrai;
q.offre(nxt);
}
}

// ---- 2. Déplacer vers le bas
si [peuvent MoveDown(grid, r, c, ori)] {
État nxt = nextDown(r, c, ori);
si (!visité[nxt.r][nxt.c][nxt.ori]) {
visité[nxt.r][nxt.c][nxt.ori] = vrai;
q.offre(nxt);
}
}

// ---- 3. Tourner dans le sens des aiguilles d'une montre (H -> V)
si (ori) HORIZ && canRotateClockwise(grid, r, c) {
État nxt = nouvel État(r, c, VERT);
si (!visité[nxt.r][nxt.c][VERT]) {
visité[nxt.r][nxt.c][VERT] = vrai;
q.offre(nxt);
}
}

// ---- 4. Rotation dans le sens contraire des aiguilles d'une montre (V -> H)
si (ori) (grille, r, c)) {
État nxt = nouvel État(r, c, HORIZ);
Si (!visité[nxt.r][nxt.c][HORIZ]) {
visité[nxt.r][nxt.c][HORIZ] = vrai;
q.offre(nxt);
}
}
}
étapes++;
}
retour -1; // impossible
}

- Oui. Méthodes d'aide pour les quatre types de déplacement --------- */

boolean privé canMoveRight(int[][] g, int r, int c, int ori) {
int n = longueur g;
si (ori) HORIZ) {
int nc = c + 2;
retour nc < n& g[r][nc] == 0;
} autres { // verticale
retour (c + 1 < n && g[r][c + 1]] 0) &&
(c + 1 < n && g[r + 1][c + 1]] 0);
}
}

Etat privé suivantDroit(int r, int c, int ori) {
si (ori) HORIZ) retourne un nouvel État(r, c + 1, HORIZ);
retourner un nouvel État(r, c + 1, VERT);
}

Boîte de booléen privéeMoveDown(int[]] g, int r, int c, int ori) {
int n = longueur g;
si (ori) VERT) {
int nr = r + 2;
retour nr < n && g[nr][c]] 0;
} autres { // horizontale
retour (r + 1 < n && g[r + 1]]] 0) &&
(r + 1 < n && g[r + 1][c + 1]] 0);
}
}

État privé suivantDown(int r, int c, int ori) {
si (ori) VERT renvoie un nouvel État(r + 1, c, VERT);
retourner un nouvel État(r + 1, c, HORIZ);
}

boolean privé canRotateClockwise(int[]] g, int r, int c) {
int n = longueur g;
retour (r + 1 < n) &&
(g[r + 1][c] == 0 && g[r + 1][c + 1] == 0);
}

Clockwise(int[]] g, int r, int c) {
int n = longueur g;
retour (c + 1 < n) &&
[g[r][c + 1] == 0 && g[r + 1][c + 1] == 0);
}

- Oui. Catégorie d ' État
État(int r, int c, int ori) {}
}
«» "

** Harnais d'essai**

"Java
classe principale {
public statique vide principal(String[] args) {
int[[]] grille = {
[0,0,0,1]
[1,1,0,0,1,0],
{0,00,1,1,1},
{0,0,0,1,1,0},
{0,1,1,0,0,0},
{0,1,1,0,0,0}
};
System.out.println(nouvelle solution().minimumMoves(grid)); // → 11
}
}
«» "

---

5.2 Python 3.10

'`python
à partir de collections import deque
de taper l'importation Liste

Solution de classe:
HORIZ, VERT = 0, 1

def minimum Déplacement(self, grid: List[List[int]]) -> Int:
n = len(grid)
visité = [[[False]*2 pour _ in range(n)] pour _ in range(n)]
q = deque([(0, 0, self.HORIZ)]) # (ligne, col, orientation)

visité[0][0][self. HORIZ] = Vrai
étapes = 0
cible = (n-1, n-2, self. - Oui.

alors que q:
pour _ dans la plage(len(q)):
r, c, o = q.popleft()
si (r, c, o) == cible:
étapes de retour

1. Bougez à droite
si self.can_move_right(grid, r, c, o):
nr, nc, no = self.next_right(r, c, o)
si elle n'est pas visitée[nr][nc][non]:
visité[nr][nc][no] = Vrai
q.appendice((nr, nc, n))

2. Reculez
si self.can_mouve_down(grid, r, c, o):
nr, nc, no = self.next_down(r, c, o)
si elle n'est pas visitée[nr][nc][non]:
visité[nr][nc][no] = Vrai
q.appendice((nr, nc, n))

3. Tourner dans le sens des aiguilles d'une montre (H → V)
si elle est elle-même. HORIZ et self.can_rotate_cw(grid, r, c):
si elle n'est pas visitée[r][c][elle-même]. - Oui.
visité[r][c][se) lui-même. VERT] = Vrai
q.Append(r, c, self.VERT)

4. Rotation dans le sens contraire des aiguilles d'une montre (V → H)
o == Self.VERT et self.can_rotate_ccw(grid, r, c):
si elle n'est pas visitée[r][c][elle-même]. - Oui.
visité[r][c][se) lui-même. HORIZ] = Vrai
q.Append(r, c, self. HORIZ))

étapes += 1
retour -1

Méthodes d'aide - Oui.
def can_move_right(self, g, r, c, o):
n = len(g)
si elle est elle-même. - Oui.
retour c + 2 < n et g[r][c + 2] 0
# verticale
retour (c + 1 < n et g[r][c + 1]] 0 et
c + 1 < n et g[r + 1][c + 1]] 0)

def next_right(self, r, c, o):
si elle est elle-même. - Oui.
retour r, c + 1, o
retour r, c + 1, o

def can_move_down(self, g, r, c, o):
n = len(g)
si elle est elle-même. VOIR :
retour r + 2 < n et g[r + 2][c]] 0
# horizontale
retour (r + 1 < n et g[r + 1]]] 0 et
r + 1 < n et g[r + 1][c + 1]] 0)

def next_down(self, r, c, o):
si elle est elle-même. VOIR :
retour r + 1, c, o
retour r + 1, c, o

def can_rotate_cw(self, g, r, c):
n = len(g)
retour r + 1 < n et c + 1 < n et \
g[r + 1][c] == 0 et g[r + 1][c + 1]] 0

def can_rotate_ccw(self, g, r, c):
n = len(g)
retour r + 1 < n et c + 1 < n et \
g[r][c + 1] == 0 et g[r + 1][c + 1] == 0
«» "

**Complexité** – temps « O(n2) », espace « O(n2) ».



---

Numéro 5.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int minimum Déplacements(vecteur<vecteur<int>>& grille) {
const int n = quadrillage.size();
Const int H = 0, V = 1;
vecteur<vector<array<bool, 2>>> vis(n, vecteur<array<bool, 2>>(n, {faux, faux})

file d'attente<tuple<int,int,int>> q; // rang, col, orientation
q.emplacer(0, 0, H);
vis[0][0][H] = vrai;
Étapes int = 0;
const int tr = n - 1, tc = n - 2; // cible en bas à droite du bloc

pendant que (!q.vide()) {
int sz = q.size();
pendant que (sz--) {
auto [r, c, o] = q.front(); q.pop();
Si (r) tr && c == tc && o == H) les étapes de retour;

/* 1. À droite */
si (peut déplacerRight(grid, r, c, o)) {
auto [nr, nc, no] = nextRight(r, c, o);
si (!vis[nr][nc][non]) {
vis[nr][nc][no] = vrai;
q.emplacer(nr, nc, no);
}
}

/* 2. Déplacer */
si (peut MoveDown(grid, r, c, o)) {
auto [nr, nc, no] = nextDown(r, c, o);
si (!vis[nr][nc][non]) {
vis[nr][nc][no] = vrai;
q.emplacer(nr, nc, no);
}
}

/* 3. Tourner dans le sens des aiguilles d'une montre (H -> V) */
si (o) H & & canRotateCW(grid, r, c)) {
si (!vis[r][c][V]) {
vis[r][c][V] = vrai;
q. mettre en place(r, c, V);
}
}

/* 4. Rotation dans le sens contraire des aiguilles d'une montre (V -> H) */
si (o) V & & canRotateCCW(grid, r, c) {
si (!vis[r][c][H]) {
vis[r][c][H] = vrai;
q. mettre en place(r, c, H);
}
}
}
+ étapes;
}
retour -1;
}

particulier:
Const int H = 0, V = 1;

Méthodes d'aide
bool canMoveRight(vecteur const<vector<int>>& g, int r, int c, int o) {
int n = g.size();
Si (o) H) { // horizontale
retour c + 2 < n && g[r][c + 2] == 0;
} // verticale
retour (c + 1 < n && g[r][c + 1]]
c + 1 < n& g[r + 1][c + 1]] 0);
}

tuple<int,int,int> nextRight(int r, int c, int o) {
retour {r, c + 1, o};
}

bool canMoveDown(vecteur commun<vector<int>>& g, int r, int c, int o) {
int n = g.size();
si (o == V) { // verticale
retour r + 2 < n && g[r + 2][c]] 0;
} // horizontale
retour (r + 1 < n && g[r + 1]]]
r + 1 < n && g[r + 1][c + 1]] 0);
}

tuple<int,int,int> nextDown(int r, int c, int o) {
retour {r + 1, c, o};
}

Bool canRotateCW(const vector<vector<int>>& g, int r, int c) {
int n = g.size();
retour r + 1 < n && c + 1 < n &&
[r + 1][c] == 0 && g[r + 1][c + 1] == 0;
}

Bool canRotateCCW(const vector<vector<int>>& g, int r, int c) {
int n = g.size();
retour r + 1 < n && c + 1 < n &&
g[r][c + 1] == 0 && g[r + 1][c + 1] == 0;
}
};
«» "

**Utilisation**

'`cpp
Int main() {
vector<vector<int>> grille = {
[0,0,0,1]
[1,1,0,0,1,0],
{0,00,1,1,1},
{0,0,0,1,1,0},
{0,1,1,0,0,0},
{0,1,1,0,0,0}
};
nombre d'heures de travail par semaine;
}
«» "

---

---

- Oui. 6. Discussion – parties de bonne / mauvaise

Aspect (Ce que nous avons bien fait)
C'est-à-dire...
**État explicite** Exclusivement Représenté par `(row, col, orientation)` – facile à hacher et à visiter. Oublier de vérifier *deux* cellules après une rotation. Autres
**Déplacer les contrôles de légalité**Déplacer chaque mouvement a un petit assistant indépendant – aucune logique dupliquée. Mélange d'indices pour les mouvements horizontaux et verticaux. Autres
**Le traitement de la couche BFS** En utilisant une seule file d'attente et en oubliant de boucler sur `size()`. Autres
**Conditions limites** Erreurs hors-par-un dans `c+2 < n` ou `r+2 < n`.
**L'espace**=2-D visité tableau *par* orientation → O(n2). Utiliser `unordered_set` de tuples ajouterait des frais généraux. Autres

---

- Oui. 7. À emporter pour les intervieweurs et les candidats

* Le problème se résume à **grid navigation avec une pièce coulissante/rotation**.
* Un BFS sur un espace d'état 3-D (`row × col × orientation`) le résout dans le temps `O(n2)`.
* Faites attention aux quatre conditions de déplacement** – elles sont la seule subtilité.
* Éviter les erreurs d'index : Vérifiez toujours l'index **maximum** avant d'accéder à la grille.

---

- Oui. 8. Verdict final

C'est un puzzle d'interview classique qui teste:

1. ** Représentation de l'État** – modélisation de l'orientation du bloc.
2. **Manipulation globale** – éviter les erreurs hors-par-un.
3. ** Pensée algorithmique** – BFS sur un petit espace d'état.

Une fois que vous écrivez les quatre vérifications d'aide, le reste est mécanique. Les trois implémentations ci-dessus devraient obtenir un **5/5** parfait sur une entrevue de codage typique.

Bon codage ! C'est ce qu'il a dit.

---

**Mots clés:** `navigation par réseau`, `bloc glissant`, `BFS`, `orientation`, `rotation`, `LeetCode`, `Programmation dynamique`, `C++`, `Python`, `Java`.