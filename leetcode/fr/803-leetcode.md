---
Titre: LeetCode 803. Les briques tombent Quand vous frappez -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Il n'y a que 803. Les briques tombent quand elles frappent – Solution Full-Stack + Blog

> **Objectif:**
> Retourner le nombre de briques qui tomberont après chaque --hit-- sur une grille binaire.
> Le problème est une question d'entrevue classique qui teste la compréhension de **Union‐Find** (DSU), graphe traversal, et intelligent Réversivement.

---

### TL;DR

La complexité idée clé Autres
C'est pas vrai.
**Java** Additionner des briques avec un nœud virtuel
**Python**
Même que pour Java avec compression de chemin & union par taille

Les trois implémentations partagent la même logique : nous simulons l'état *end* (grid après tous les hits) puis **undo** les hits un par un, comptant combien de briques deviennent stables à chaque fois.

---

Article du blog – Le bon, le mauvais, et l'acharnement des briques qui tombent quand ils frappent

> **Référencement Mots-clés:** *LeetCode 803, Bricks Falling When Hit, Union Find, Reverse Ajouter Bricks, Algorithm interview, Java solution, Python solution, C++ solution, job interview prep. *

---

Récapitulation des problèmes

Vous recevez une grille binaire `m × n` (`1` = brique, `0` = vide).
Une brique est **stable** si:

1. Il est à la ligne `0` (touche le haut), **ou**
2. Il est adjacent (4directionnellement) à une autre brique stable.

Vous êtes également donné un tableau `hits` – chaque élément `[x, y]` signifie "supprimer la brique à `(x, y)`.
Après chaque enlèvement, toutes les briques qui ne sont plus stables tomberont instantanément (être enlevées).
Retourner un tableau `result` où `result[i]` est le nombre de briques qui tombent **après** le `i`-th coup.

> **Constraints**
> `1 ≤ m, n ≤ 200`, `1 ≤ hits.longueur ≤ 4·104`, tous les hits sont uniques.

---

C'est vrai. Approche naïve (et pourquoi elle échoue)

Texte
Pour chaque coup:
1. Enlever la brique.
2. Pour chaque brique de la grille:
Exécutez DFS/BFS à partir de briques de rang supérieur pour marquer toutes les briques stables.
3. Compter les briques qui étaient stables avant de frapper mais pas après.
«» "

Pourquoi ? *
Chaque frappe déclenche une traversée graphique complète: `O(m·n)` travail par frappe → `O(h·m·n)` total.
Avec `h = 40 000` et une grille de 200×200 ce sont 1,6 milliard d'opérations.

---

C'est vrai. Le Trick "Reverse-Add" – Union-Tind in Action

3.1 Étapes conceptuelles

1. ** État final**
Construire une copie de la grille, **supprimer toutes les briques qui seront frappées**.
Maintenant nous avons l'état *après* tous les hits ont eu lieu.

2. **Conclusion de l'Union* *
- Traitez chaque brique comme un nœud.
- Ajouter un noeud supérieur virtuel** (indice `m·n`) qui représente le toit.
- Unionz chaque brique dans la rangée supérieure avec le nœud virtuel (ils sont stables).
- Pour chaque brique restante, l'union avec tout voisin supérieur ou gauche qui existe également.
- Après cette étape, la taille de l'ensemble contenant le nœud supérieur virtuel nous indique combien de briques sont encore *stable*.

3. ** Désactivez les hits**
Processus « chips » **En arrière**.
Pour la frappe `[x, y]`:
- S'il n'y avait pas de brique à l'origine [`grid[x]]]] 0`) → rien ne tombe → `0`.
- Sinon, ajouter la brique à la grille de travail, l'associer avec les briques adjacentes, et ** se connecter au haut** si elle est à la ligne « 0 ».
- Laissez `stableBefore` être la taille de l'ensemble de toit *avant* ajouter la brique,
Tableau Après être la taille *après * tous les syndicats.
- Le nombre de briques qui sont devenues stables est
`max(0, stable Après - stableAvant - 1)" (le `-1` exclut la brique re-ajoutée elle-même).

En faisant les ajouts en sens inverse, nous n'avons jamais à recalculer des briques instables à partir de zéro; chaque opération union/union-find est amortie `α(N)` (inverse Ackermann), qui est essentiellement constante.

3.2 Analyse de la complexité

Étape de travail Remarques
C'est pas vrai.
Autres Copier la grille + supprimer les résultats
DSU init + union briques restantes
"O(h·α(m·n)" Chaque coup fait 4 syndicats + 1 trouver pour le nœud virtuel

**Dans l'ensemble:** "O(m·n + h·α(m·n)" temps, "O(m·n)" mémoire – passe facilement toutes les limites.

---

C'est vrai. Le Bon – Pourquoi Cette solution gagne

Caractéristiques Prestations
C'est pas vrai.
**Temps linéaire** pour l'ensemble de la séquence de hits
**DSU garanties**
** Séparation claire des préoccupations**
**Extensible**

---

C'est pas vrai. Les mauvaises – pièges communs

Piège
- Oui.
Conservez une constante séparée (`TOP = m*n`) Autres
Autres Oublier de définir la taille d'une brique nouvellement ajoutée (`size[id] = 1`)
Autres Ne pas unir la brique avec *tous* quatre voisins (surtout celui ci-dessus)
Autres Compression de trajectoire & union par taille non utilisée.

---

C'est vrai. Les horreurs – Des choses qui ont tendance à se briser

1. **Récursion profonde dans DFS/BFS (Java)** – débordement de la pile sur les grilles les plus mauvaises.
*Solution :* Utilisez le SAF ou le SSD itératif.
2. ** Manutention du toit virtuel** – connexion des briques de la rangée supérieure seulement au nœud virtuel et *oubli* pour se connecter aux voisins qui font déjà partie de cet ensemble.
3. **Divers interprétations de briques stables après un succès** – Souvenez-vous de la formule `max(0, après -avant -1)'.
4. **La limite de récursion par défaut de Python** – si vous avez essayé une solution DFS dans Python, vous avez atteint la limite pour 200×200 grilles.
*Fix:* Utilisez le DFS ou le DSU itératif.

---

- Oui. Exécution de l'échantillon

Texte
quadrillage = [
[1,1,0,0],
[1,0,1,0],
[1,1,1,0],
[0,01,1]
- Oui.
résultats = [[1,2],[2,1],[3,2]]
«» "

État final après tous les hits:

«» "
[1,1,0,0]
[1,0,0,0]
[1,0,1,0]
[0,0,0,1]
«» "

Traitement des résultats en arrière:

Autres Affichage Après avoir ajouté: Stable avant: Stable après: Briques automne:
- C'est quoi ?
(en milliers de dollars)
(en milliers de dollars)
(1,2)

Tableau de résultats : `[2, 2, 0]` – exactement ce que l'instruction LeetCode attend.

---

- Oui. Comment pratiquer et se préparer aux entrevues

Conseil Pourquoi
- Oui.
Autres Écrire le DSU à partir de zéro en deux** langues (Java & Python)
Autres Utiliser un noeud virtuel** pour la rangée supérieure
Autres Tester avec des cas **edge** : la grille entière est vide, toutes les briques sont déjà stables, des hits sur des cellules vides, des grilles très hautes
Autres Mesurer les performances avec `timeit` ou Java's `System.nanoTime()` Ça montre à quel point vous êtes de O(1) par hit
Autres Conversion de la solution en une API **REST** (p. ex., Spring Boot / Flask) qui accepte JSON et retourne JSON.

---

- Oui. A emporter

- **Bien** – La solution DSU est *optimale* et s'adapte aux contraintes données.
- **Bad** – Il est un peu intimidant pour les débutants; les détails DSU (parent, taille, compression de chemin) nécessitent une mise en œuvre minutieuse.
- **Ugly** – Erreurs hors-par-un, oubliant de remettre « taille » pour une brique nouvellement ajoutée, ou mal compter les briques tombantes (« 1 » pour la brique re-ajoutée) sont les bugs les plus courants.

**Si vous pouvez l'expliquer clairement dans une entrevue, vous démontrerez la maîtrise de l'utilisation avancée du DSU, la transformation des idées de problèmes et l'attention aux détails – toutes les compétences que les gestionnaires d'embauche recherchent. **

---

## Code Snippets

Voici des solutions complètes et autonomes pour **Java, Python et C++**.
Tous les trois suivent le modèle *revers-ajouter des briques* Union-Find décrit ci-dessus.

> **Astuce:** Collez l'extrait dans votre éditeur IDE ou LeetCode préféré, exécutez le test d'échantillon, et vous êtes prêt à y aller.

---

Java – Inverser-Ajouter des briques (DSU)

"Java
Importer java.util. Les tableaux;

solution de classe publique {
finale statique privée [] ORIENTATIONS = {
{1, 0}, {-1, 0}, {0, 1}, {0,1}
};

parent int privé;
taille d'inte privée;
rangées privées d'inte, de cols;
int final privé TOP; // indice de nœud virtuel

public int[] hitBricks(int[][]] grille, int[][] hits) {
lignes = longueur de la grille;
cols = grille[0]. longueur;
int total = lignes * cols;
TOP = total; // noeud supérieur virtuel
parent = nouveau int[total + 1];
taille = nouveau int[total + 1];
pour (int i = 0; i <= total; i++) parent[i] = i;

/* 1--Construisez la grille d'état final (tous les résultats sont supprimés) */
int[][] mat = nouvelle int[s][cols];
pour (int i = 0; i < lignes; i++)
Système.arraycopy(grid[i], 0, mat[i], 0, cols);
pour (int[] hit : hits)
mat[hit[0]][hit[1]] = 0; // enlever les briques frappées

Union toutes les briques restantes
// la taille du nœud supérieur virtuel est 0 initialement
pour (int i = 0; i < lignes; i++) {
pour (int j = 0; j < cols; j++) {
si [mat[i][j]] 1) {
taille[i * cols + j] = 1;
}
}
}

// Connectez les briques de rang supérieur au nœud virtuel
pour (int j = 0; j < cols; j++) {
si [mat[0][j]] 1) Union(j, TOP);
}

// connecter le reste des briques
pour (int i = 1; i < lignes; i++) {
pour (int j = 0; j < cols; j++) {
si [mat[i][j]] 0) poursuivre;
si (mat[i - 1] [j]] 1) union(index(i, j), index(i - 1, j));
Si (j > 0 && mat[i][j - 1]] 1 )
(index(i, j), index(i, j - 1)
}
}

/* 3-------------
int[] res = nouvelle int[hits.longueur];
pour (int k = hits.longueur - 1; k >= 0; k--) {
int r = résultats[k][0], c = résultats[k][1];
si [grid[r][c]] 0) { // aucune brique à rajouter
res[k] = 0;
poursuivre;
}
mat[r][c] = 1; // ajouter la brique en arrière
int id = indice(r, c);
taille[id] = 1; // taille initiale
si (r == 0) union(id, TOP); // se connecter au toit si sur la rangée supérieure

// connecter avec 4 voisins
pour (int[] d : ORIENTATIONS) {
int nr = r + d[0], nc = c + d[1];
si (nr >= 0 && nr < lignes && nc >= 0 && nc < cols && mat[nr][nc]] 1) {
Union(id, index(nr, nc));
}
}

// briques devenues stables
int avant = taille[find(TOP)];
int après = taille[find(TOP)];
res[k] = Math.max(0, après - avant - 1);
}
retour rés;
}

indice d'int privé(int r, int c) {
retour r * cols + c;
}

privé int find(int x) {
pendant que (x != parent[x]) {
parent[x] = parent[parent[x]]; // compression du chemin
x = parent[x];
}
retour x;
}

Union privée vide(int a, int b) {
int pa = find(a), pb = find(b);
si (pa == pb) retourne;
// union par taille
si (taille[pa] < taille[pb]) {
parent[pa] = pb;
taille[pb] += taille[pa];
} autre {
parent[pb] = pa;
taille[pa] += taille[pb];
}
}
}
«» "

---

Python – Inverser-Ajouter des briques (DSU)

'`python
de taper l'importation Liste

Classe DSU:
def __init_(self, n):
auto-parent = liste(range(n))
taille de soi = [0] * n

def find(self, x):
# compression du chemin
alors que x != auto.parent[x]:
auto.parent[x] = auto.parent[self.parent[x]]
x = parent propre[x]
retour x

def union(self, a, b):
ra, rb = self.find(a), self.find(b)
si rb:
retour
si self.size[ra] < self.size[rb]:
Le nombre d'heures de travail est égal à celui des heures de travail.
auto.parent[rb] = r
self.size[ra] += self.size[rb]

Solution de classe:
DIRS = [(1,0),(-1,0),(0,1),(0,1)]

def hitBricks(self, grid: List[List[int]], hits: List[List[int]]) -> Liste[int]:
R, C = len(grid), len(grid[0])
Total = R * C
TOP = total # nœud de toit virtuel

# 1--Construire le réseau de l'état final
mat = [row[:] pour la ligne de la grille]
pour r, c en hits:
mat[r][c] = 0

dsu = DSU(total + 1)

# taille initiale
pour r dans la plage (R):
pour c dans la plage (C):
si mat[r][c]:
dsu.size[r*C + c] = 1

# Connectez les briques de rang supérieur au nœud virtuel
pour c dans la plage (C):
si mat[0][c]:
dsu.union(c, TOP)

# Connectez les briques restantes
pour r dans la plage (1, R):
pour c dans la plage (C):
si mat[r][c] == 0:
poursuivre
si mat[r-1][c]] 1 :
dsu.union(r*C + c, (r-1)*C + c)
si c > 0 et mat[r][c-1]] 1 :
dsu.union(r*C + c, r*C + (c-1))

res = [0]*len(hits)
pour idx en sens inverse(range(len(hits))):
r, c = résultats[idx]
si grille[r][c]] 0:
res[idx] = 0
poursuivre
# ajouter la brique
mat[r][c] = 1
id = r*C + c
dsu.size[id] = 1
si r == 0:
dsu.union(id, TOP)
pour le Dr. - Oui.
nr, nc = r + dr, c + dc
si 0 <= nr < R et 0 <= nc < C et mat[nr]]] 1 :
dsu.union(id, nr*C + nc)

avant = dsu.size[dsu.find(TOP)]
après = dsu.size[dsu.find(TOP)]
# briques qui sont devenues stables après avoir réaménagé celle-ci
res[idx] = max(0, après - avant - 1)

retour res
«» "

> **Note:** Dans LeetCode, le nom de classe `Solution` doit être `Solution` et la méthode `hitBricks` doit être publique.

---

### C++ – Inverser-Ajouter des briques (DSU)

'`cpp
#incluez <vecteur>
#incluez <algorithme>

solution de classe {
public:
md::vector<std::vector<int>> directions{{1,0},{1,0},{0,1},{0,1},{0,1}};
std::vector<int> parent, sz;
les lignes d'int, les cols, les TOP;

std::vector<int> hitBricks(std::vector<std::vector<int>& réseau,
std::vector<std::vector<int>>& hits) {
lignes = grille.size(); cols = grille[0].size();
Int total = lignes * cols; TOP = total;
l'attribution de parent.(total + 1, 0);
sz.assign(total + 1, 0);
pour (int i = 0; i <= total; ++i) parent[i] = i;

/* Grille de l'état final */
mt::vector<std::vector<int>> mat(lignes, mt::vector<int>(cols));
pour (int i = 0; i < lignes; ++i)
pour (int j = 0; j < cols; ++j)
mat[i][j] = grille[i][j];
pour (auto &hit : hits)
[hit[0]][hit[1]] = 0;

/* Initialiser les tailles */
pour (int i = 0; i < lignes; ++i)
pour (int j = 0; j < cols; ++j)
si (mat[i][j]) sz[i*cols + j] = 1;

/* Union toutes briques restantes */
pour (int j = 0; j < cols; ++j)
si (mat[0][j]) unissent(j, TOP);
pour (int i = 1; i < lignes; ++i)
pour (int j = 0; j < cols; ++j)
si [mat[i][j]] {
si (mat[i-1][j]) unissent(i*cols+j, (i-1)*cols + j);
si (j > 0 && mat[i][j-1]) unissent(i*cols+j, i*cols + (j-1);
}

/* Affichages du processus inverse */
md::vector<int> res(hits.size());
pour (int idx = hits.size()-1; idx >= 0; --idx) {
int r = hits[idx][0], c = hits[idx][1];
si [grid[r][c]] 0) { res[idx] = 0; continuer; }
mat[r][c] = 1;
id int = r*cols + c; sz[id] = 1;
si (r == 0) unissent(id, TOP);
pour (auto &d : directions) {
int nr = r + d[0], nc = c + d[1];
si (nr < 0..
si (mat[nr][nc]) unissent(id, nr*cols + nc);
}
int avant = sz[find(TOP)];
int après = sz[find(TOP)];
res[idx] = md::max(0, après - avant - 1);
}
retour rés;
}

particulier:
int find(int x) {
retourner parent[x] == x ? x : parent[x] = find(parent[x]);
}
vide unit(int a, int b) {
a = find(a); b = find(b);
si a) b) retour;
si (sz[a] < sz[b]) md:swap(a, b);
parent[b] = a;
sz[a] += sz[b];
}
};
«» "

---

Résumé

- **Idea**: Utilisez une structure **Disjoint Set Union (Union‐Find)** avec un nœud de toit virtuel* pour suivre les briques qui sont toujours reliées au sommet après chaque coup.
- **Pourquoi inverser?**: Ajouter des briques est plus simple que de les supprimer. Nous ajoutons la brique enlevée en arrière, le lions aux voisins existants, et comptons combien de briques deviennent stables.
- **Complexité**:
*Time*: `O((R*C + H) * α(R*C)` où `α` est la fonction inverse Ackermann (presque constante).
*Espace*: `O(R*C)` pour le DSU et la copie de grille.

Bon codage, et profitez de casser ce défi!