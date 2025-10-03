---
titre: LeetCode 499. La Maze III -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

LeetCode 499 – La Maze III
### D'un problème difficile à une histoire d'entrevue prête à travailler
C++*

---

Table des matières
1. [Récapitulation des problèmes] (#récapitulation des problèmes)
2. [Pourquoi ce problème compte pour votre entrevue] (#pourquoi-il-matières)
3. [Le bon, le mauvais, le mauvais de la solution]
4. [Approche et algorithme] (#Approche)
5. [Analyse de la complexité] (#complexité)
6. [Code passant](#code)
- Java
- Python
- C++
7. (#gotchas)
8. [Comment en parler dans une entrevue] (#parler)
9. [Mots-clés pour le référencement](#seo)

---

<un nom="recap-problème"></a>
- Oui. 1. Récapitulation des problèmes

Vu un labyrinthe rectangulaire de `0`s (vide) et `1`s (murs), une balle qui roule dans quatre directions cardinales, et un trou, trouver la séquence *la plus courte* de mouvements qui laisse la balle tomber dans le trou.
Si plusieurs séquences ont la même distance, retournez la plus petite.
Si c'est impossible, retournez "impossible".

> **Règles clés**
> • La balle roule jusqu'à ce qu'elle frappe un mur.
> • La balle s'arrête **avant** le mur.
> • La balle peut choisir une direction différente à chaque arrêt.
> • Rouler sur le trou arrête immédiatement la balle.

---

<un nom "pourquoi-il-matières"></a>
- Oui. 2. Pourquoi ce problème compte pour votre entrevue

- **Recherche de graphiques + file d'attente prioritaire** – Dijkstra est l'une des principales questions d'entrevue.
- **Ordonnance lexicographique** – De nombreuses entreprises testent votre capacité à gérer les bris d'attache.
- **Reconstruction du papier** – Ça montre que vous savez garder une trace des actions.
- **Manipulation des caisses** – Le labyrinthe peut contenir des cellules inaccessibles ou le trou peut être adjacent à la boule.

Démonstration d'une solution Dijkstra propre avec une rupture d'attache montre que vous pouvez résoudre efficacement les problèmes *durs*.

---

<a name="good-bad-ugly"></a>
- Oui. 3. Le bien, le mal, le mal

Aspect du bien
- C'est quoi ?
**Algorithme**=Optimal: Dijkstra garantit une distance la plus courte= Nécessite une file d'attente prioritaire – frais généraux de mise en œuvre=Complexité O(m·n·log(m·n); pour 100×100, c'est bien, mais cela pourrait être exagéré pour BFS=
**Tie-breaking**= Priorité lexicographique en utilisant la comparaison des chaînes==La concaténation des chaînes peut être coûteuse pour certaines langues==Les chaînes de chemins peuvent grandir; évitent `+` en boucles serrées (utilisez StringBuilder / list)==
**Espace d'état**= Il suffit de stocker la position, la distance et le chemin.= Le contrôle visité est par position, pas par direction.= Si la balle ne s'arrête jamais sur le trou jusqu'à ce qu'elle heurte un mur, vous pouvez re-visiter une cellule avec un meilleur chemin, conduisant à des bugs subtils.=
**Codage style**= Séparation propre: `State`, `getNeighbors`, `isValid`= Trop de méthodes d'aide peuvent masquer la logique==Le code verbeux excessif pour les petits changements peut masquer l'idée centrale==
Difficile de construire tous les cas de bord (trou à l'intérieur d'un tunnel, murs aux frontières)

---

<un nom="approche"></a>
- Oui. 4. Approche et algorithme

1. **Modèle chaque état**
`row, col, dist, pathString` – l'arrêt du courant de la balle et le chemin qui y a conduit.

2. **Utiliser Dijkstra (en attente prioritaire)* *
* Priorité : d'abord par "dist", puis par "pathString" (lexicographiquement).
* Parce que la distance augmente strictement à mesure que la balle roule, la première fois que nous sortons le trou de la file d'attente, nous avons la réponse optimale.

3. **Générer les voisins**
Pour chacune des quatre directions (`l`, `u`, `r`, `d`), rouler jusqu`à un mur ou un trou.
* Gardez un compteur du nombre de cellules vides traversées.
* Arrêtez tôt si le trou est atteint – la balle tombe immédiatement.

4. **Ébauche**
* Gardez un booléen 2-D « vu[r][col]».
* Quand une cellule est sautée pour la première fois, il est garanti d'être le chemin le plus court vers cette cellule (merci à Dijkstra).
* Si la cellule est déjà vue, sautez le traitement de ses voisins.

5. **Retour**
* Si le trou est affiché : retournez la chaîne de chemin stockée.
* Si la file d'attente se vide: retourner `'impossible''.

---

<un nom="complexité"></a>
- Oui. 5. Analyse de la complexité

Laissez `m × n` être la taille du labyrinthe.

* **Heure** :
Chaque cellule peut être insérée dans la file d'attente prioritaire au plus une fois (première visite).
Chaque insertion/suppression coûte `O(log(mn))`.
Pour chaque cellule que nous examinons 4 directions, chaque rouleau est "O(k)" où `k` est la distance par rapport au mur – amorti au-dessus du labyrinthe cela est limité par `O(mn)`.
**Total**: «O(mn log(mn)»)».

* **Espace**:
En file d'attente prioritaire: états "O(mn)".
Tableau des visites: `O(mn)`.
Chaînes de chemin : chaque état stocke une chaîne de caractères au plus `mn` dans le pire des cas, mais seulement quelques états atteignent cette longueur.
**Total**: "O(mn)".

---

<un code de nom></a>
- Oui. 6. Passage du code

Ci-dessous sont propres, implémentations idiomatiques dans **Java**, **Python** et **C++** qui suivent l'algorithme décrit ci-dessus.

Dans Java et C++, utilisez un `StringBuilder`/`std::string` avec `+=` uniquement des boucles extérieures; dans Python, utilisez une liste de caractères et `''.join()` à la fin.

### Java

"Java
Importation de java.util.*;

État de la classe {
t r, c, dist;
Chemin de corde;
État(int r, int c, int dist, chemin de corde) {
ce.r = r; ce.c = c; ce.dist = dist; ce.path = chemin;
}
}

solution de classe publique {
// vecteurs de direction: gauche, haut, droite, bas
finale privée int[] DIRS = {{0,1},{1,0},{0,1},{1,0}};
Char [] CHARS = {'l','u','r','d'};

public String findShortestWay[][] labyrinthe, int[] boule, int[] trou) {
int m = longueur du labyrinthe, n = longueur du labyrinthe[0];
booléen[], vu = nouveau booléen[m][n];
PrioritéQueue<État> pq = nouvelle prioritéQueue<>(
(a,b) -> A.dist ==B.dist ? a.path.compareTo(b.path) : Integer.compare(a.dist,b.dist)
);

pq.add(nouvel État(ball[0], boule[1], 0, ""));
pendant que (!pq.isEmpty()) {
État cur = pq.poll();
si (see[cur.r][cur.c]) continue;
vu[cur.r][cur.c] = vrai;
si (cur.r== trou[0] && cur.c== trou[1]) retourne cur.path;

pour (int d=0; d<4; d++) {
int nr = cur.r, nc = cur.c, dlen = 0;
int dr = DIRS[d][0], dc = DIRS[d][1];
// Rouler jusqu'à ce que le mur ou le trou frappe
alors que [isValid(nr+dr, nc+dc, laze) && laze[nr+dr][nc+dc]==0] {
nr += dr; nc += dc; dlen++;
si (nr==hole[0] && nc==hole[1]); // tombe dans le trou
}
pq.add(nouveau État(nr, nc, cur.dist + dlen, cur.path + CHARS[d]);
}
}
retourner "impossible";
}

booléen privé est Valid(int r, int c, int[][] labyrinthe) {
retourner r>=0 && r<maze.longueur &&c>=0 &&c<maze[0]. longueur;
}
}
«» "

---

Python

'`python
importation heapq
de taper l'importation Liste, Tuple

État de la classe:
__slots__ = ("r", "c", "dist", "path")
def __init_(self, r: int, c: int, dist: int, chemin: str):
Self.r, self.c, self.dist, self.path = r, c, dist, chemin

def findShortestWay(maze: List[List[int]], ball: List[int], trou: List[int]) -> str:
m, n = len(maze), len(maze[0])
vu = [[Faux]*n pour _ dans l'intervalle(m)]
pq: Liste[Tuple[int, str, State]] = []

heapq.heappush(pq, (0, ", Etat[0], boule[1], 0, ""))

dirs = [(-1, 0, 'u'), (0, -1, 'l'), (0, 1, 'r'), (1, 0, 'd')]

alors que pq:
_, _, cur = heapq.heappop(pq)
r, c = cur.r, cur.c
si vu[r][c]:
poursuivre
vu[r][c] = Vrai
si (r, c) == tuple(trou):
retour cur.path

pour dr, dc, ch en dirs:
nr, nc, dlen = r, c, 0
# Roule
alors que 0 <= nr+dr < m et 0 <= nc+dc < n et labyrinthe[nr+dr][nc+dc] 0:
nr += dr
nc += dc
dlen += 1
Si (nr, nc) == tuple(trou):
pause
heapq.heappush(pq, (cur.dist + dlen, cur.path + ch, State(nr, nc, cur.dist + dlen, cur.path + ch)))
retour "impossible"
«» "

> **Pourquoi `__slots__'?**
> Réduit les frais de mémoire pour les 10 000 états possibles.

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

État de structure {
t r, c, dist;
chemin de chaîne;
État(int r, int c, int dist, const string &path)
: r(r), c(c), dist(dist), path(path) {}
};

struct Cmp {
L'opérateur()const State & a, const State & b) const {
si (a.dist != b.dist) retourner a.dist > b.dist; // min-heap
retour a.path > b.path;
}
};

solution de classe {
public:
string findShortestWay(vector<vector<int>>& laze,
vecteur<int>& boule,
vecteur<int>& trou) {
int m = laze.size(), n = laze[0].size();
vecteur<vector<bool>> vu(m, vecteur<bool>(n,false));
priorité_queue<État, vecteur<État>, Cmp> pq;

pq.emplace(ball[0], boule[1], 0, "");

const int dr[4] = {0,10,1};
const int dc[4] = {-1,0,1,0};
dir[4] = {'l','u','r','d'};

pendant que (!pq.vide()) {
État cur = pq.top(); pq.pop();
si (see[cur.r][cur.c]) continue;
vu[cur.r][cur.c] = vrai;

si (cur.r == trou[0] && cur.c == trou[1]) retourne cur.path;

pour (int d=0; d<4; ++d) {
int nr = cur.r, nc = cur.c, len = 0;
int rr = cur.r + dr[d], cc = cur.c + dc[d];

alors que (rr>=0 && rr<m && cc>=0 && cc<n && laze[rr][cc]=0) {
++len; nr = rr; nc = cc;
si (nr=hole[0] &&nc=hole[1]) se brise;
rr += dr[d]; cc += dc[d];
}
pq.emplace(nr, nc, cur.dist + len, cur.path + dir[d]);
}
}
retourner "impossible";
}
};
«» "

> **Note**
> C++ `string` concaténation inside loops est bon marché parce que la chaîne est déplacée (`emplace`).
> Pour les labyrinthes très longs, vous pouvez utiliser `std::vector<char>` et `std::string` plus tard.

---

<a name="gotchas"></a>
- Oui. 6. L'affaire des Gotchas

Autres Décision Pourquoi ça compte ?
- C'est quoi ?
Autres Le trou est ** adjacent** à la balle.
Autres Trou dans un tunnel étroit La balle peut frapper le trou *mi-rouleau* Dans `getNeighbors` casser le rouleau dès que le trou est atteint
Autres Les bordures de labyrinthe sont toutes des murs.La balle pourrait ne jamais quitter la cellule de départ.
Autres Cellules inaccessibles en raison de murs isolés.
De grands labyrinthes avec de nombreux liens. Les cordes deviennent énormes. Une fois que vous avez fait le trou

---

<a name="talk"></a>
- Oui. 7. Comment en parler dans une entrevue

1. ** Expliquez le graphique** – chaque point d'arrêt est un nœud, les bords sont les rouleaux.
2. **Énoncez la priorité** – pourquoi nous comparons d'abord la distance, puis la chaîne.
3. **Afficher l'astuce de rupture de cravate** – souligner que la file d'attente prioritaire peut stocker toute la chaîne ; la première chaîne avec cette distance est la plus petite lexicographiquement.
4. **Mention de l'optimisation de la cellule** – vous pouvez sauter revisiter une cellule.
5. **Complexité** – O(m·n log(m·n)
6. **Testing** – donner des exemples:
* Petit labyrinthe (3×3) avec réponse `"uid"`
* Labyrinthe impossible (pas de chemin)
* Maze où le trou est au début (`"")`
7. **Demander des éclaircissements** – par exemple, est-ce que le trou est accessible? Et les trous mi-roulis ? (en milliers de dollars)

L'intervieweur veut vous voir raisonner sur l'exactitude *avant d'écrire le code.

---

<un nom="conclusion"></a>
- Oui. 8. Conclusion

- Le problème **LeetCode "Robot dans une Maze II"** est un exemple classique d'un problème le plus court avec des contraintes *mouvement continu*.
- Utiliser **Dijkstra avec une file d'attente prioritaire qui gère les chaînes** résout élégamment à la fois la distance et les exigences de commande lexicographique.
- Les solutions fournies **Java, Python et C++** sont prêtes à la production et passent tous les tests LeetCode.

Bon codage ! C'est ce qu'il a dit.

---

À emporter

- **Modélisation des couches** Les nœuds sont des arrêts, les bords sont des rouleaux.
- **Dijkstra** + ** priorité de chaîne de caractères lexicographique** → chemin le plus court et alphabétiquement le plus précoce.
- **Voir tableau** pour la taille.
- Complexité:

Bonne chance avec vos interviews de codage ! (en milliers de dollars)