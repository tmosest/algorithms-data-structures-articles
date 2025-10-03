---
Titre: LeetCode 1559. Détecter les cycles dans la grille 2D -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
#1559. Détecter les cycles dans la grille 2D
**LeetCode – Medium – Java / Python / C++ solutions + SEO-optimized blog post**

> **Mots clés** – Détecter les cycles dans la grille 2D, LeetCode 1559, DFS BFS détection de cycle, Grid graph, Job interview, Structures de données, Algorithmes, Java DFS, Python DFS, C++ BFS

---

- Oui. 1. Aperçu du problème

On vous donne une grille 2-D `grid[m][n]` de lettres anglaises minuscules.
Un **cycle** est un chemin de longueur **≥ 4** que :

* ne visite que des cellules ayant le même caractère,
* ne bouge que dans les 4 directions cardinales,
* retourne à la cellule de départ,
* ** Ne retourne jamais dans la cellule dont tu viens de venir**.

Retourner `true` si un tel cycle existe, sinon `faux`.

«» "
m, n ≤ 500 → grille peut contenir jusqu'à 250 000 cellules
«» "

La tâche est un problème graph-théorie classique sur une grille : détecter un cycle dans un graphique non dirigé où les sommets sont des cellules avec la même lettre.

---

- Oui. 2. Les bons, les mauvais, les méchants

Aspect du bien
- C'est quoi ?
**Algorithme**Le DFS (récursion) est intuitif et facile à mettre en œuvre. BFS fonctionne également avec une file d'attente de `(row, col, parentRow, parentCol)`. DFS et BFS doivent explorer chaque cellule une fois ; pour les grandes grilles, la profondeur de récursion peut atteindre les limites en Python ou en Java. Une approche naïve qui revisite les cellules ou qui ne vérifie pas l'état de «parent» ne signale pas correctement les cycles. Autres
**Complexité du temps**= O(m · n) – chaque cellule est visitée une fois. Aucun – linéaire est optimal pour ce problème. Certaines solutions utilisent par erreur `O(m · n)^2)` en raison de scans répétés. Autres
Autres **Complexité de l'espace**.O(m · n) pour le tableau visité + pile de récursion / file d'attente. Utiliser `HashMap` pour chaque cellule peut souffler la mémoire. Autres
**Readability** Le DFS récursif peut masquer la logique parentale aux nouveaux arrivants. Des implémentations surcomplètes de la recherche syndicale détournent l'idée de base. Autres
**Le rendement**Le DFS en Java (récursion « O(1) » par appel) fonctionne < 100 ms sur LeetCode. BFS avec une classe de paires personnalisées peut être plus lent en Java en raison de la boxe/déboîte. Autres

---

- Oui. 3. Aperçu algorithmique

Traitez la grille comme un graphique non dirigé où chaque cellule est un nœud.
Deux nœuds sont adjacents s'ils partagent un côté et contiennent la même lettre.

Lors d'une première traversée en profondeur:

* Lorsque vous explorez un voisin `(nr, nc)` de la cellule actuelle `(r, c)`,
* Si le voisin n'a pas été visité**, revenir avec `(r, c)` comme parent.
* Si le voisin ** a été visité** et que ce n'est pas le parent**, un cycle existe.

Le contrôle de la marque « Parent » garantit que nous ne détectons pas faussement le trivial chemin de retour et de retour de deux cellules comme un cycle.

---

- Oui. 4. Mise en œuvre du code

> Toutes les solutions partagent la même logique ; seule la syntaxe diffère.

### 4.1 Java – DFS (récursif)

"Java
Importation de java.util.*;

solution de classe {
Int[] dr = {1, -1, 0, 0};
int[] dc = {0, 0, -1, 1};

booléen public contientCycle(char[]] grille) {
int m = longueur de grille, n = longueur de grille[0];
int[]] vis = nouveau int[m][n]; // 0 = non visité, 1 = visité
pour (int i = 0; i < m; i++) {
pour (int j = 0; j < n; j++) {
si [vis[i][j]] 0) {
Si [dfs(grid, vis, i, j, -1, -1, grille[i]]]
retour vrai;
}
}
}
retourner faux;
}

Booléen privé dfs[] g, int[]] vis,
Int r, int c,
Int pr, int pc,
Couleur de l'omble) {
vis[r][c] = 1;
pour (int k = 0; k < 4; k++) {
int nr = r + dr[k], nc = c + dc[k];
si (nr < 0=0 nr >= g.longueur
poursuivre;
si (g[nr][nc] != couleur) continuer;
si [vis[nr][nc]] 0) {
si (dfs(g, vis, nr, nc, r, c, couleur) retourner vrai;
} sinon si (nr != pr==== nc!= pc) { // visité et non parent
retour vrai;
}
}
retourner faux;
}
}
«» "

> **Astuce pour les interviews Java** – utilisez `int[][] vis` au lieu d'un `boolean[][]` afin que vous puissiez stocker la coordination parent indirectement (par exemple, encoder `(r, c)` dans un seul entier) si vous voulez éviter de passer parent séparément.

---

#### 4.2 Python – DFS (pierre itérative)

'`python
de taper l'importation Liste

Solution de classe:
def contient Cycle(self, grille: List[List[str]]) -> bool:
m, n = len(grid), len(grid[0])
vis = [[Faux]*n pour _ dans l'intervalle(m)]
dirs = [(1,0), (-1,0), (0,1), (0,-1)]

pour i dans la plage (m):
pour j dans la plage(n):
si non vis[i][j]:
pile = [(i, j, -1, -1)] # (r, c, parent_r, parent_c)
vis[i][j] = Vrai
pendant la pile:
r, c, pr, pc = pile.pop()
pour dr, dc en dirs:
nr, nc = r+dr, c+dc
si 0 <= nr < m et 0 <= nc < n et quadrillage[nr]] quadrillage[r][c]:
si non vis[nr][nc]:
vis[nr][nc] = Vrai
(nr, nc, r, c))
élif nr != p ou nc != pc:
retour Vrai
Retour Faux
«» "

> ** Pourquoi itératif?** La limite de profondeur de récursion de Python (par défaut 1000) se briserait pour les grandes grilles; une pile explicite des marches secondaires que.

---

### 4.3 C++ – DFS (récursif)

'`cpp
solution de classe {
Const int dr[4] = {1, -1, 0, 0};
const int dc[4] = {0, 0, -1, 1};

public:
bool contient Cycle(vecteur<vecteur<char>>& grille) {
int m = quadrillage(), n = quadrillage[0].size();
vecteur<vector<int>> vis(m, vecteur<int>(n, 0));

pour (int i = 0; i < m; ++i) {
pour (int j = 0; j < n; ++j) {
si (!vis[i][j]) {
Si [dfs(grid, vis, i, j, -1, -1, grille[i]]]
retour vrai;
}
}
}
retourner faux;
}

particulier:
bool dfs(vector<vector<char>>&g, vecteur<vector<int>>& vis,
nt r, int c, int pr, int pc, char col) {
vis[r][c] = 1;
pour (int k = 0; k < 4; ++k) {
int nr = r + dr[k], nc = c + dc[k];
Si (nr < 0) nr >= (int)g.size()) nc < 0) nc >= (int)g[0].size()
poursuivre;
si (g[nr][nc] != col) continue;
si (!vis[nr][nc]) {
si (dfs(g, vis, nr, nc, r, c, col))
retour vrai;
} sinon si (nr != pr==== nc != pc) { // visité, pas parent
retour vrai;
}
}
retourner faux;
}
};
«» "

> **Note pour les interviews C++** – attention avec la taille de la pile; utilisez `std::vector` pour le tableau `vis` et passez par référence.

---

- Oui. 5. Analyse de la complexité

Algorithme Temps Espace
- C'est quoi ?
DFS (toutes langues confondues) **O(m · n)**
**O(m · n)** – file d'attente + tableau visité

Les deux sont linéaires et optimales; la grille peut être visitée une fois.

---

- Oui. 6. Article du blog – Détecter les cycles dans une grille 2-D : le bon, le mauvais, le mauvais

> **Méta—Description* *
> Code maître de leet 1559 Détecter les cycles dans la grille 2-D avec les solutions Java, Python et C++. Apprenez la meilleure stratégie, les pièges et pourquoi ce problème est un must-savoir pour votre prochaine entrevue sur les structures de données.

---

6.1 Introduction

Si vous vous préparez à des entrevues techniques, les cycles de destruction dans la grille 2-D sont des éléments essentiels.
Il mélange graphe traversal, suivi parent, et contrôles prudents des limites — tous dans les contraintes d'une grille 500 × 500.

> **Pourquoi c'est important** – De nombreux intervieweurs demandent des variations de détection du cycle (liste liée, graphiques, grilles). La maîtrise démontre votre capacité à adapter un algorithme de base à différents modèles de données.

---

6.2 Le problème revisité

*(Insérer la déclaration officielle avec le bloc de code.) *

---

6.3 Les bonnes

1. **FDS est naturel** – Traitez chaque cellule comme un nœud ; deux nœuds sont connectés s'ils partagent un côté * et* contiennent la même lettre.
2. **Linear runtime** – O(m · n) est le plus rapide que vous pouvez obtenir.
*LeetCodeS test data* s'exécute généralement en < 100 ms.
3. **Simple logique parent** – En passant les coordonnées de la cellule précédente, vous savez immédiatement si un voisin visité est le parent.
*Un seul drapeau booléen dans votre tableau `visited` est insuffisant; vous devez vérifier la direction. *

> **Pro tip** – Écrivez un helper `dfs(r, c, parent_r, parent_c)` qui retourne `True` dès qu'un cycle est trouvé. Pas besoin de revenir sur les résultats après avoir exploré tous les enfants.

---

Les mauvais

Question Conséquences Correction
- Oui.
Sens de récursion supérieur à 250 000 (Python, Java) Autres
Autres Oubliant l'état de « parent » Faux positifs (p. ex., deux cellules arrière et quatre) Toujours comparer les coordonnées du voisin au parent avant de déclarer un cycle. Autres
Utiliser une seule matrice visitée; une fois une cellule marquée, sautez-la. Autres

---

6.5 La moche

> Certains candidats écrivent un code qui, bien que logiquement correct, est **messy**:

1. **Union‐Trouver sur une grille* *
*Dépassé pour un simple problème de DFS. *
Il introduit des abstractions lourdes (compression de chemin, rang) qui distraient de la logique centrale.
2. ** Structures de données inutiles* *
*Utiliser `HashSet<(int,int)>` pour chaque cellule ou une carte clé par la lettre. *
Ça fait exploser la mémoire pour 250 k cellules.
3. ** Directions codées en dur**
*En utilisant des tableaux `int` séparés pour `dr` et `dc` dans chaque fonction. *
Bien que rapide, il peut être caché derrière les boucles imbriquées et les boucles mal indexées.

> **Takeaway** – Gardez votre solution maigre : une matrice visitée, un tableau de direction et un contrôle parent.

---

### 6.6 Conseils pour réussir l'entrevue

La langue Stratégie Cas de bord
C'est pas vrai.
Utiliser `int[]] vis` et coder parent comme un seul entier si la profondeur de récursion est une préoccupation. Rappelez-vous de réinitialiser la visite lorsque vous terminez un composant. Autres
*Python * Préférez une pile explicite; évitez la récursion. Augmentation de la limite de récursion (sys.setrecursionlimit) *seulement* si vous êtes confiant sur la profondeur de la pile. Autres
**C++**= Passer les vecteurs par référence; être explicite sur les contrôles aux frontières (`r+dr < m`). Utiliser `std::vector<int>` pour `vis` au lieu de `bool` pour éviter les questions signées/non signées. Autres

---

6.7 Analogies du monde réel

La détection de cycle sur une grille est comme trouver une boucle dans un labyrinthe où vous pouvez seulement marcher à travers des murs de la même couleur.
Imaginez une grille de ville où vous ne pouvez voyager que dans des rues peintes de la même couleur; un cycle est une promenade fermée qui ne retrace jamais immédiatement une étape.

---

6.8 Réflexions finales

- **Mise en oeuvre une fois, testez beaucoup** – Écrire le DFS dans n'importe quelle langue, exécutez-le sur les trois exemples officiels de LeetCode.
- ** Vérifier l'état parent** – C'est le cœur de la solution; manquant, c'est le bug le plus commun.
- ** Gardez-le linéaire** – Toute tentative quadratique est un drapeau rouge pour l'évaluation de l'exécution et de l'entrevue.

Avec ces extraits de Java, Python et C++ dans votre boîte à outils, vous allez vous attaquer avec confiance au LeetCode 1559 et démontrer la maîtrise de la détection de cycle – une compétence clé pour toute interview d'algorithme.

---

### 6.9 Appel à l'action

> ** Prêt à monter à niveau? **
> Ajouter ce message, télécharger les extraits de code, et ajouter le problème à votre liste quotidienne de pratiques. (en milliers de dollars)
> Besoin d'aide avec un autre classique LeetCode ? Laissez un commentaire ou envoyez-moi un courriel — heureux de vous aider à vous préparer à votre prochaine entrevue de codage!

---

- Oui. 7. Conclusion

LeetCode 1559 est simple une fois que vous comprenez:

* Traiter la grille comme un graphique non dirigé,
* DFS avec suivi des parents,
* Temps linéaire et espace.

Les solutions Java, Python et C++ ci-dessus illustrent une implémentation propre qui passera tous les tests officiels et impressionnera les intervieweurs.

Bon codage – et bonne chance pour votre prochaine entrevue! C'est ce qu'il a dit.

---

* Fin de l'article. *