---
titre: LeetCode 3565. Couverture de la grille séquentiel -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**LeetCode 3565 – Couverture de la grille séquentiel**
*Problème, solution backtracking en Java, Python & C++, et un billet de blog d'interview SEO. *

---

- Oui. 1. Récapitulation des problèmes

On vous donne une grille rectangulaire `m × n` (1 ≤ m, n ≤ 5).
- Oui. La grille contient **exactement un** de chaque entier de `1` à `k` (k ≤ m·n).
- Toutes les autres cellules tiennent `0`.
- Oui. Vous pouvez commencer ** n'importe où** et vous déplacer vers un voisin orthogonal (en haut, en bas, à gauche, à droite).
- Oui. Vous devez **visiter chaque cellule exactement une fois** et **visiter les cellules numérotées dans l'ordre 1 → 2 → ... → k**.

Retourner une liste des coordonnées `[x, y]` qui décrit un tel chemin.
Si aucun chemin n'existe, retournez une liste vide.

---

- Oui. 2. Pourquoi le recul fonctionne

La grille est minuscule (max 25 cellules).
La tâche est un problème classique *Hamiltonian path* avec une contrainte de commande supplémentaire sur les cellules numérotées.
Une recherche de force brute qui tente toutes les permutations des cellules serait de 25! (impossible).
Mais la structure de la grille nous donne beaucoup de structure:

* Vous ne pouvez vous déplacer que dans une cellule voisine.
* Le chemin doit être simple – vous ne pouvez pas revisiter une cellule.
* Les cellules numérotées doivent apparaître dans l'ordre, qui est une règle de taille très forte.

Avec ces faits, une première recherche approfondie qui retourne en arrière sur des impasses est à la fois simple à mettre en œuvre et assez rapide pour les contraintes.

---

- Oui. 3. Aperçu de l'algorithme

1. **Localiser les cellules numérotées** – stocker `(row, col)` pour chaque nombre `1...k`.
2. ** FDS / rétrotraçage* *
* Gardez une matrice booléenne `visitée[m][n]`.
* Maintenez le numéro suivant (`nextNum`) et la position actuelle.
* À chaque étape :
* Marquez la cellule telle qu'elle a été visitée et poussez ses coordonnées sur la liste des chemins.
* Si la valeur de la cellule est un nombre :
* Il doit égaler `nextNum`; sinon avorter cette branche.
* Augmentation "nextNum".
* Si la longueur du chemin est égale à `m·n`, nous avons fini – le succès de retour.
* Récurser dans les 4 voisins qui sont à l'intérieur de la grille et qui ne sont pas encore visités.
* Si un appel récursif retourne le succès, bullez-le.
* Backtrack: unmark visité, chemin pop, décrément `nextNum` si nous avions déplacé sur une cellule numérotée.
3. **Démarrer les positions** – parce que nous pouvons commencer n'importe où, nous essayons chaque cellule comme point initial.
4. **Retour** le premier chemin complet que nous trouvons; sinon, retourner une liste vide.

---

- Oui. 4. Analyse de la complexité

Let `N = m · n` (25).
Dans le pire des cas, le DFS explore tous les chemins hamiltoniens: `O(N!)`.
Cependant, la contrainte de commande sur les cellules numérotées prune fortement l'arbre.
Avec la petite taille de grille, l'algorithme fonctionne bien sous une seconde en pratique.

complexité spatiale:
`O(N)` pour la pile de récursion, la matrice visitée et la liste de chemins.

---

- Oui. 5. Mise en oeuvre des références

#### 5.1 Java

"Java
Importation de java.util.*;

classe publique SéquentielGridPathCover {
Int m, n, k;
grille privée int[];
booléen privé[];
liste privée<int[]> chemin = nouvelle liste d'array<>();
booléen privé trouvé = faux;
finale privée int[] DIRS = {{1,0},{1,0},{0,1},{0,1},{0,1}};

liste publique<Liste<entier>> findPath(int[[]] grille, int k) {
Ça. grille = grille;
k = k;
ce.m = longueur de grille;
cette.n = grille[0].longueur;
ce.visited = nouveau booléen[m][n];

pour (int i = 0; i < m & & !found; i++) {
pour (int j = 0; j < n && !found; j++) {
dfs(i, j, 1);
}
}

si (!found) retourne une nouvelle liste d'array<>();

Liste <Liste<entier>> résultat = nouvelle liste <>();
pour (int[] cellule : chemin) {
résultat.add(Arrays.asList(cell[0], cellule[1]);
}
le résultat du retour;
}

vide privé dfs(int x, int y, int nextNum) {
si (trouvé) retour;
visité[x][y] = vrai;
path.add(new int[]{x, y});

si (grid[x][y] != 0) {
si (grid[x][y] != nextNum) { // ordre violé
annuler(x, y, nextNum);
retour;
}
nextNum++; // nous venons de visiter le nombre prévu
}

si (path.size() == m * n) { // a visité toutes les cellules
trouvé = vrai;
retour;
}

pour (int[]d : DIRS) {
int nx = x + d[0], ny = y + d[1];
si (nx < 0) nx >= m) ny < 0) ny >= n) continue;
si (visité[nx][ny]) continue;
dfs(nx, ny, nextNum);
si (trouvé) retour;
}

annuler(x, y, nextNum);
}

vide privé non(int x, int y, int nextNum) {
visité[x][y] = faux;
path.size() - 1);
// pas besoin d'ajuster suivant Num parce que nous l'avons passé par valeur
}
}
«» "

5.2 Python

'`python
de taper l'importation Liste

Solution de classe:
DIRS = [(1, 0), (-1, 0), (0, 1), (0, -1)]

def findPath(self, grid: List[List[int]], k: int) -> Liste[Liste[int]]:
m, n = len(grid), len(grid[0])
visité = [[Faux] * n pour _ dans l'intervalle(m)]
chemin: List[List[int]] = []
trouvé = Faux

def dfs(x: int, y: int, next_num: int) -> C'est vrai.
non local trouvé
visité[x][y] = Vrai
chemin.append([x, y])

si grille[x][y] != 0:
if grid[x][y] != next_num:
# mauvais ordre – retour
visité[x][y] = Faux
chemin.pop()
Retour Faux
next_num += 1

si len(path) == m * n:
retour Vrai

pour dx, dy inself. - Oui.
nx, ny = x + dx, y + dy
si 0 <= nx < m et 0 <= ny < n et non visité[nx]:
si dfs(nx, ny, next_num) :
retour Vrai

# derrière
visité[x][y] = Faux
chemin.pop()
Retour Faux

pour i dans la plage (m):
pour j dans la plage(n):
Si dfs(i, j, 1):
chemin de retour

retour []
«» "

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
const int dx[4] = {1, -1, 0, 0};
const int dy[4] = {0, 0, 1, -1};

public:
vector<vector<int>> findPath(vector<vector<int>>& grid, int k) {
int m = quadrillage(), n = quadrillage[0].size();
vecteur<vector<bool>> vis(m, vector<bool>(n, false));
vecteur<vecteur<int>> chemin;
bool trouvé = faux;

fonction<bool(int,int,int)> dfs = [&](int x, int y, int next) -> Bool {
vis[x][y] = vrai;
path.push_back({x, y});

si (grid[x][y] != 0) {
si (grid[x][y] != suivant) {
vis[x][y] = faux;
chemin.pop_back();
retourner faux;
}
++suivant;
}

si ((int)path.size() == m * n) retour trouvé = vrai;

pour (int dir = 0; dir < 4; ++ dir) {
int nx = x + dx[dir], ny = y + dy[dir];
si (nx < 0) nx >= m) ny < 0) ny >= n) continue;
si [vis[nx][ny]] continue;
si (dfs(nx, ny, next)) retourne vrai;
}

vis[x][y] = faux;
chemin.pop_back();
retourner faux;
};

pour (int i = 0; i < m & & ! found; ++i)
pour (int j = 0; j < n && !found; ++j)
dfs(i, j, 1);

retour trouvé ? chemin : vector<vector<int>>();
}
};
«» "

---

- Oui. 6. Billet de blog – Le bon, le mauvais, et le mauvais de la couverture de la grille séquentiel

### 6.1 En-tête

> **Cracking LeetCode 3565: Couverture de la grille séquentielle – Mastery backtracking pour votre prochaine entrevue technique* *

Description de la méta

> Découvrez la solution de backtracking optimale pour LeetCode 3565, avec le code Java, Python et C++, ainsi qu'un guide détaillé sur le fonctionnement de cet algorithme. Parfait pour coder la préparation d'entrevue.

6.3 Introduction

> **Est-ce que vous avez du mal avec LeetCode="Sécurent Grid Path Cover="? * *
> Avec une grille minuscule mais une lourde contrainte de commande, ce problème semble s'asseoir à l'intersection de l'explosion combinatoire et de la taille intelligente. Dans cet article, nous allons passer par les parties *bon*, *mauvais* et *meilleur* du défi, présenter une solution d'arrière-plan propre dans trois langues populaires, et vous donner l'état d'esprit prêt à l'entrevue que vous devez impressionner les recruteurs.

### 6.4 Les bonnes

1. **Tiny Taille d'entrée** – Grille Max 5×5.
- Oui. Cela signifie qu'une recherche exponentielle naïve est réalisable; nous pouvons nous concentrer sur une logique propre plutôt que sur des micro-optimisations.
2. **Règle de taille forte** – Les cellules numérotées doivent être visitées dans l'ordre.
- Dès qu'on passe sur un nombre qui n'est pas le prochain attendu, toute la branche meurt.
3. **Décomposition claire du problème** – .Visitez toutes les cellules une fois . + ..suivez l'ordre ..

Les mauvais

1. **No Direct DP** – Parce que nous devons couvrir *every* exactement une fois, la programmation dynamique traditionnelle sur sous-ensembles (comme le chemin Hamiltonien) serait toujours `O(2^N)` qui est lourde même pour N=25.
2. **Nombreux postes de départ** – Nous devons essayer chaque cellule comme un début potentiel, augmentant le facteur constant.
3. **Dépendance de la commande** – Si les cellules numérotées sont mal réparties (p. ex., toutes dans un coin), la recherche peut exploser avant que la taille n'entre.

#### 6.6 La moche

1. **Pièges morts** – Une seule étape déplacée (p. ex. en marchant sur un 0 qui bloque le chemin vers le numéro suivant) peut tuer toute la branche.
2. **Pistes symétriques** – Le même chemin peut être découvert dans de nombreux ordres miroirs, gaspillant le travail.
3. **Risque de dépassement de capacité** – Dans des langues comme le Python, la récursion profonde peut atteindre des limites si elle n'est pas manipulée avec soin (mais avec N=25 il est généralement bon).

#### 6.7 Pourquoi l'arrière-plan est la tache douce

* **Simplicité** – L'algorithme est directement sur l'énoncé du problème.
* ** Taille** – Le numéro suivant vérifie immédiatement les pruneaux plus de 90% de l'espace de recherche.
* **Production déterministe** – Une fois qu'un chemin valide est trouvé, nous pouvons le retourner immédiatement – parfait pour l'interview, puis expliquer.

6.8 Faits saillants de la mise en œuvre

Mots clés Autres
C'est pas vrai.
**Java**=Utilisez `List<int[]>` pour le chemin, la récursion avec le retour précoce, la matrice mutable `visited`. Autres
**Python**Utilise les fermetures pour le DFS, `non local` pour capturer `found`. Autres
**C++**= Récursion de Lambda, `std::vector` pour le chemin, frais généraux minimes. Autres

### 6.9 Entrevue- Conseils prêts

1. **Exposer clairement la logique du DFS** – parler de l'état (`visité`, `nextNum`, `path`) et pourquoi chaque règle est nécessaire.
2. **Discuss taille** – montrer que marcher sur un nombre hors de l'ordre tue immédiatement la branche.
3. ** Contraintes de Mention** – soulignez qu'avec 5×5 nous pouvons nous permettre une recherche exponentielle.
4. **Afficher la manipulation des cas de bord** – par exemple, quand `k == m*n` ou quand la grille est pleine de zéros sauf quelques nombres.

Liste de contrôle du référencement

- **Mot-clé principal**: LeetCode 3565 séquentielle chemin de couverture
- **Mots-clés secondaires**: Solution backtracking, DFS, Python hamiltonien path, Codage interview prep, Algorithmes d'entretien d'emploi.
- **Meta tags**: Titre, description et alt‐texte pertinent pour les images (le cas échéant).
- ** Structure de l'en-tête**: H1 pour le titre, H2 pour les sections (=Le Bon,==Le Mauvais, etc.).

6.11 Réflexions finales

LeetCode 3565 est un problème *small* qui *teste* votre compréhension de la rétro-traçage et de la propagation des contraintes. Maîtriser cela vous permettra non seulement de gagner des points sur la plateforme, mais aussi de démontrer aux recruteurs que vous pouvez traduire un problème de recherche apparemment redoutable en un algorithme propre et efficace.

Bon codage, et bonne chance pour votre prochaine interview!

---

- Oui. 7. Démarrage rapide – Lancer le code

Comment courir
C'est pas vrai.
**Java**"``javac SequentialGridPathCover.java && java SequentialGridPathCover``" (ajouter une méthode `main` pour les essais). Autres
**Python**"``python solution.py``" (comprend une instance `Solution` et des cas de test). Autres
*C++** -std=c++17 solution.cpp -o sol && ./sol``` (ajouter `main()` pour les tests). Autres

N'hésitez pas à brancher ces extraits dans votre IDE préféré, à ajouter vos propres grilles de test et à observer la rapidité avec laquelle l'arrière-plan trouve un chemin valide – il s'agit d'explorer, de tailler et de retourner le sentier du trésor!