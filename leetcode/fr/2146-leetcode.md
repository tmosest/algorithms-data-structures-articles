---
titre: LeetCode 2146. K Les articles les plus classés dans une fourchette de prix -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Algorithmes – Mise en œuvre en 3 langues

Vous trouverez ci-dessous une mise en œuvre propre et prête à la production du problème de la voie la plus précieuse** (LeetCode 2143) dans **Java, Python et C++**.
Les trois solutions suivent la même stratégie de haut niveau:

1. **La première recherche (BFS)** depuis la cellule de départ – nous garantissons que nous visitons les cellules à une distance croissante de Manhattan.
2. **Taille minimale / file d'attente prioritaire** qui maintient la cellule suivante à examiner selon les quatre règles de classement
(distance, prix, ligne, colonne).
3. Quand le prix d'une cellule se situe dans `[faible, élevé]` nous l'ajoutons à la liste de réponses jusqu'à ce que nous ayons des résultats `k`.

La mise en œuvre utilise une structure «visitée» pour éviter de revoir les cellules (un «boolean[]]» en Java/C++ et un «set» en Python).
La complexité est **O(N log N)** temps et **O(N)** espace auxiliaire, où `N = R × C` (le nombre de cellules traversables).

---

#### 1.1 Java

"Java
Importation de java.util.*;

solution de classe publique {

int final statique privé[] DIR = {1, 0, -1, 0, 1};

Liste publique<Liste<entier>> Plus hautRankedKItems(
int[] [] grille, int[] tarification, int[] départ, int k) {

int R = longueur de grille, C = longueur de grille[0];
Int low = prix[0], high = prix[1];
int sx = début[0], sy = début[1];

// Cellules visitées
booléen[][] visité = nouveau booléen[R][C];
visité[sx][sy] = vrai;

// Min–heap: {dist, prix, ligne, col}
PriorityQueue<int[]> tas = nouveau PriorityQueue<>(
(a, b) -> a[0] != b[0] ? a[0] - b[0] :
a[1] != b[1] ? a[1] - b[1] :
a[2] != b[2] ? a[2] - b[2] :
a[3] - b[3]);

// file d'attente BFS
Queue<int[]> q = nouveau ArrayDeque<>();
q.offre(nouvelle int[]{0, grille[sx][sy], sx, sy});

Liste <Liste<Intégrée>> ans = nouvelle liste <>();

pendant que (!q.isEmpty() && ans.size() < k) {
[] cur = q.poll();
dist = cur[0], prix = cur[1], r = cur[2], c = cur[3];

si (faible <= prix && prix <= élevé) {
as.add(Arrays.asList(r, c));
}

pour (int d = 0; d < 4; ++d) {
int nr = r + DIR[d];
int nc = c + DIR[d + 1];
si (nr < 0. C) poursuivre;
si [grid[nr][nc]] == 0=" visité[nr][nc]) continue;
visité[nr][nc] = vrai;
q.offre(nouvelle int[]{dist + 1, grille[nr][nc], nr, nc});
}
}

le retour des an;
}
}
«» "

*Pourquoi `PriorityQueue` + BFS? *
La file d'attente prioritaire garantit que les cellules apparaissent dans l'ordre correct des règles de classement, tandis que BFS garantit que nous visitons les cellules à distance croissante.
Aucun tri de toutes les cellules n'est nécessaire, de sorte que l'algorithme reste rapide même pour la limite de 100 k-cell.

---

#### 1.2 Python

'`python
importation heapq
de taper la liste d'importation, Tuple, Set

Solution de classe:
le plus haut ClasséKItems(
soi-même,
grille: Liste[Liste[int]],
prix: Liste[int],
début : Liste[int],
k: int
) -> Liste [Liste[int]]:
R, C = len(grid), len(grid[0])
faible, élevé = prix
sx, sy = début

# Min-heap: (distance, prix, ligne, col)
heap: Liste[Tuple[int, int, int, int]] = [(0, grille[sx][sy], sx, sy)]
visité: Set[Tuple[int, int]] = {(sx, sy)}

ans: Liste[Liste[int]] = []

pendant le tas et le len(ans) < k:
dist, prix, r, c = heapq.heappop(heap)

si faible <= prix <= élevé:
Annexe([r, c])

pour dr, dc dans ((1, 0), (-1, 0), (0, 1), (0, -1):
nr, nc = r + dr, c + dc
si 0 <= nr < R et 0 <= nc < C \
et quadrillage[nr][nc] > 0 et (nr, nc) non visités:
visité.add((nr, nc))
heapq.heappush(heap, (dist + 1, quadr[nr][nc], nr, nc))

retour et
«» "

*Pourquoi un "set" pour visite? *
La grille peut être aussi grande que les cellules `1e5`; un `boolean[][]` consommerait une quantité comparable de mémoire. Un "set" de tuples maintient l'utilisation de la mémoire serrée tout en fournissant des recherches O(1).

---

*## 1.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

Numéro de structure {
Dénomination des marchandises
prix int;
à r, c;
Noeud(int d, int p, int r, int cc) : dist(d), p, r(rr), c(cc) {}
};

struct cmp {
Bool operator()(const Node&a, const Node&b) const {
si (a.dist != b.dist) retourner a.dist > b.dist;
si (a.prix != b.prix) retourner a.prix > b. prix;
si (a.r != b.r) retourner a.r > b.r;
retour a.c > b.c;
}
};

solution de classe {
public:
vecteur<vecteur<int>> Plus hautRankedKItems(
vecteur<vecteur<int>& grille,
le vecteur<int> et la tarification,
vecteur<int> et début,
Int k) {

int R = quadrillage.size(), C = quadrillage[0].size();
Int low = prix[0], high = prix[1];
int sx = début[0], sy = début[1];

vecteur<vector<bool>> vis(R, vector<bool>(C, false));
vis[sx][sy] = vrai;

priorité_queue<Node, vecteur<Node>, cmp> pq;
file d'attente<pair<int,int>> bfs; // stocke seulement les coordonnées
bfs.push({sx, sy});
dist = 0;

// BFS pour calculer la distance à chaque cellule accessible
vecteur<pair<int,int>> dirs = {{1,0},{-1,0},{0,1},{0,1}};
vectorielle<vector<int>> distMat(R, vectorielle<int>(C, -1));
distMat[sx][sy] = 0;

pendant que (!bfs.vide()) {
auto [x, y] = bfs.front(); bfs.pop();
int d = distMat[x][y];
int p = grille[x][y];
si (faible <= p && p <= élevé)
pq.emplace(d, p, x, y);

pour (auto [dx, dy] : dirs) {
int nx = x + dx, ny = y + dy;
si (nx < 0) nx >= R) ny < 0) ny >= C) poursuivre;
si [grid[nx][ny]] == 0=" vis[nx][ny]] continue;
vis[nx][ny] = vrai;
distMat[nx][ny] = d + 1;
bfs.push({nx, ny});
}
}

vecteur<vecteur<int>> ans;
pendant que (!pq.vide() && k--) {
Numéro cur = pq.top(); pq.pop();
(c'est-à-dire qu'il n'y a pas d'écart entre les valeurs de référence et celles de référence)
}
le retour des an;
}
};
«» "

> **Astuce** – Si vous voulez éviter le tableau `distMat`, poussez simplement la distance avec le noeud dans la file d'attente prioritaire comme nous le faisons dans les solutions Java/Python. Le nombre de couches BFS (`dist`) peut être incrémenté à la volée.

---

- Oui. 2. Billet de blog – LeetCode 2143 : Pourquoi BFS + Min‐Heap est l'arme secrète

Titre
**=BFS + Min-Heap: Mastering LeetCode 2143 (Piste la plus précieuse) – 3-Langue Plongée profonde**

### Méta-Description
*Solve le problème dur LeetCode 2143 en Java, Python et C++ avec un algorithme éprouvé. Apprenez les règles de classement, pourquoi un petit tas compte, et comment éviter les pièges communs. Prêt à impressionner les recruteurs?

---

2.1 Introduction

Lorsque vous touchez le problème de chemin le plus précieux (LeetCode 2143), le premier instinct est souvent de trier simplement toutes les cellules. Les deux approches fonctionnent, mais elles sont soit *low* pour la limite de 100 k-cellule ou *mémory-hungry*.

Et s'il y avait un tour qui garantit **O(N log N)** temps et une petite empreinte de mémoire? L'astuce est **Breadth‐First Search (BFS) + un Min‐Heap (first file d'attente prioritaire)** – un modèle qui réapparaît dans chaque grand système-conception et interview algorithme.

---

2.2 Récapitulation du problème

> *On vous donne une grille rectangulaire, une portée `[faible, haute]`, une position de départ et un nombre `k`.
> Vous devez retourner les coordonnées des premières cellules `k` qui ont un prix dans la gamme, triées par:*

1. *Distance manhattane depuis le début*
2. *Prix (plus petit en premier)*
3. *Numéro de ligne*
4. *Numéro de colonne*

> *Si moins de cellules `k` sont accessibles, rendez-les toutes. *

---

2.3 Pourquoi les règles de classement sont cruciales

Les quatre règles signifient que vous pouvez simplement prendre les cellules les moins chères – vous devez respecter la distance d'abord.
Si vous triez tout par prix seul, vous allez briser la règle #1.
Si vous utilisez BFS seul, vous allez briser la règle #2–#4 parce que vous devriez faire un tri supplémentaire après la traversée.

---

2.4 Le bien – Pourquoi Cette approche fonctionne

Pourquoi ça gagne ?
- Oui.
**La distance est garantie**=BFS visite les cellules couche par couche, donc la première fois que nous atteignons une cellule que nous savons déjà qu'elle a la distance minimale possible. Autres
Autres **Commandé par prix / ligne / col **= Une minute garde la meilleure cellule *prochaine* dans le temps O(log N). On n'a jamais besoin de trier toute la liste. Autres
**Mémoire linéaire**.Seuls les cellules visitées (= 100 k) sont stockées. Pas de tableau dense `distMat` nécessaire en Java/Python. Autres
**Trois codes prêts à la langue**Le motif est le même dans Java, Python et C++; les recruteurs aiment voir que vous pouvez traduire des algorithmes. Autres

---

### 2.5 L'erreur commune qui brise votre solution

Qu'est-ce qui peut mal se passer ? Autres
- Oui.
Autres **L'utilisation d'un vecteur de taille R×C pour la distance**.En C++ ou Java, un tableau 2-D de cellules de 100 k peut encore être OK, mais si vous ajoutez un autre `distMat` il multiplie l'utilisation de la mémoire. Autres
**Pas de marquage visité avant de pousser jusqu'à la file d'attente** Autres
Autres **Comparer seulement la distance dans le tas**= Si vous oubliez d'incorporer le prix, la ligne ou la colonne dans le comparateur, la réponse sera erronée. Autres
**Using `pop()` au lieu de `top()`**.En C++, vous devez pop seulement après avoir récupéré l'élément; sinon le tas peut se rétrécir prématurément. Autres

---

#### 2.6 Les cas de bord qui s'effondrent

Comment se protéger contre lui
- C'est quoi ?
**Le démarrage est déjà hors de portée**L'algorithme fonctionne toujours: nous vérifions le prix *avant* nous développons les voisins. Autres
Autres **Toutes les cellules sont zéro (injoignables)**.La file d'attente BFS se terminera immédiatement, et nous retournerons une réponse vide. Autres
* "k" est plus grand que le nombre de cellules accessibles**.Nous retournons simplement toutes les cellules valides – l'état de la boucle («ans.size() < k») s'en occupe. Autres
Autres **Large `R × C` mais peu de cellules accessibles**.Notre ensemble visité maintient la mémoire basse; seules les cellules accessibles sont insérées dans le tas. Autres

---

2.7 Mise en œuvre dans 3 langues – une référence rapide

Langue Structure des données clés Complexité
- C'est quoi ?
Autres Java-ArrayDeque + PriorityQueue<int[]>` O(N log N)
Python "heapq" + "set" O(N log N)
*C++ *(N log N)

> ** Conseil professionnel :** Lors de l'écriture des éléments de tas, entreposez la distance avec le noeud. De cette façon, vous évitez un tableau séparé `distMat` et gardez le nettoyeur de code.

---

2.8 Réflexions finales – Conseils d'entrevue

1. ** Expliquer les règles de classement d'abord.** Les intervieweurs aiment un modèle verbal clair.
2. **Parcourez les couches BFS** – montrez que vous collectez la distance *avant* vous poussez un noeud dans le tas.
3. ** Mettre en évidence le comparateur min-heap** – qui est la sauce *-secrète* qui garantit l'ordre de sortie correct.
4. **Afficher les versions en trois langues** – cela démontre à la fois votre capacité de résolution de problèmes et votre polyvalence en tant que développeur.

---

2.9 Appel à l'action

> Vous voulez savoir comment résoudre *any* difficile problème LeetCode avec un code élégant et prêt à la production?
> Abonnez-vous à mon bulletin d'information pour les plongées en profondeur hebdomadaires, les vidéos de préparation d'entrevue et les défis de codage du monde réel. (en milliers de dollars)

Bon codage – et que vos traces de pile soient toujours sans erreur! C'est ce qu'il a dit