---
Titre: LeetCode 711. Nombre d'îles distinctes II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 711. Nombre d'îles distinctes II
**Hard – LeetCode**
> *=On vous donne une grille de matrice binaire m × n. Une île est un groupe de 1's (représentant des terres) reliés 4-directionnellement (horizontal ou vertical). Vous pouvez supposer que les quatre bords de la grille sont entourés d'eau.
> Une île est considérée comme la même qu'une autre si elle a la même forme, ou a la même forme après la rotation (90, 180, 270 degrés seulement) ou la réflexion (gauche/droite ou direction ascendante). Retournez le nombre d'îles distinctes.

---

Table des matières
1. [Résumé du problème] (#résumé du problème)
2. [Pourquoi cela compte pour votre recherche d'emploi](#pourquoi-il-matières)
3. [Aperçu de l'approche] (#Aperçu de l'approche)
4. [Sous-problème clé : Normalisation d'une forme d'île] (#normalisation-île)
5. [Mise en œuvre (Java-Python-C++)] (#mise en œuvre)
6. [Complexité temporelle et spatiale](#complexité)
7. [Justices et pièges] (#cas de référence)
8. [Tests et essais d'échantillons](#test)
9. [Traitements pour l'entrevue](#Tâches)
10. [Conclusion] (#conclusion)

---

<un nom="résumé des problèmes"></a>## 1. Résumé du problème
- **Input**: tableau 2-D `grid` de taille `m × n` (`1 ≤ m, n ≤ 50`) ne contenant que 0/1.
- **Output**: entier – le nombre d'îles *distinctes* en rotation et en réflexion.

Deux îles sont les mêmes si vous pouvez transformer l'une en l'autre en utilisant une séquence de rotations de 90° ou une réflexion horizontale/verticale.

---

<un nom "pourquoi-il-matières"></a>## 2. Pourquoi cela compte pour votre recherche d'emploi
- **Hard LeetCode**: Démontre la maîtrise de DFS/BFS, le hachage et la géométrie.
- **Relation avec l'industrie**: De nombreux problèmes réels concernent l'appariement de la forme (vision informatique, SIG, jeu dev).
- ** Mots-clés du référencement** : *Nombre d'îles distinctes II, LeetCode Hard, DFS, BFS, rotation, réflexion, Java, Python, C++*.

Publier un billet de blog comme celui-ci sur Medium, dev.to, ou votre site personnel peut attirer des recruteurs qui apprécient les compétences profondes de résolution de problèmes.

---

<a name="approach-overview"></a>## 3. Aperçu de l ' approche
1. **DFS / BFS** – Scanner la grille et collecter toutes les cellules appartenant à une seule île.
2. **Enregistrer les coordonnées relatives** – Pour chaque île, stocker les coordonnées relatives à la première cellule visitée.
3. ** Générer les 8 transformations** –
* 4 rotations (0°, 90°, 180°, 270°)
* Pour chaque rotation, réfléchissez également horizontalement (ou réfléchissez aussi verticalement).
4. ** Représentation canonique** – Pour chaque transformation, trier la liste des coordonnées, la convertir en chaîne (ou tuple).
5. **Cochez la chaîne minimale** – La plus petite chaîne lexicographique est la clé *canonique* pour cette île.
6. **Caisse** – Insérez la clé canonique dans un `HashSet` (ou `set` dans Python / `unordered_set` dans C++).
7. **Réponse** – La taille de l'ensemble est le nombre d'îles distinctes.

La partie critique est l'étape 4 : transformer les coordonnées de façon cohérente.

---

<un nom="normalisation-île"></a>## 4. Sous-problème clé: Normaliser une forme d'île
«» "
Étant donné un ensemble de points P = {(x1, y1), ..., (xk, yk)},
appliquer des transformations T et les normaliser.

T 1 : ( x, y) // 0°
T 2 : (-y, x) // 90°
T 3 : (-x, -y) // 180°
T 4 : (y, -x) // 270°
T 5 : (x, -y) // réflexion horizontale
T 6 : (-x, y) // réflexion verticale
«» "

Pour chaque île, nous générons les 8 ensembles `{T1(P), T2(P), ..., T8(P)} "
(se souvenir de réfléchir après chaque rotation).
Après la transformation, nous **transformons** l'ensemble de sorte que son minimum `x` et `y` soient 0.
Ensuite nous trions les points et sérialisons en une seule chaîne.
Le choix de la plus petite chaîne lexicographique garantit que toutes les îles équivalentes
produire exactement la même clé.

---

<un nom="implémentations"></a>## 5. Mise en œuvre

Ci-dessous sont **trois solutions complètes, prêtes à composer** – une dans chaque Java, Python et C++.
Tous utilisent le DFS itératif (stack) pour éviter les limites de récursion, mais le DFS récursif fonctionnerait aussi bien pour les contraintes données.

> **Conseil** – Gardez votre code propre : séparez la logique de transformation en fonctions d'aide.
> Cela rend le code plus facile à lire et à tester.

---

#### 5.1 Java (Java 17+)

"Java
Importation de java.util.*;

solution de classe publique {
Int public numDistinctIslands2(int[[]]) {
int m = longueur de grille, n = longueur de grille[0];
booléen[]] vis = nouveau booléen[m][n];
Set<String> vu = nouveau HashSet<>();

int[] dx = {1, -1, 0, 0};
int[] dy = {0, 0, 1, -1};

pour (int i = 0; i < m; ++i) {
pour (int j = 0; j < n; ++j) {
si (grid[i][j]== 1 && !vis[i][j]) {
Liste<int[]> île = nouvelle liste d'array<>();
Stack<int[]> st = nouveau Stack<>();
st.push(nouvelle int[]{i, j});
vis[i][j] = vrai;

pendant que (!st.isEmpty()) {
Int[] cur = st.pop();
l'île.add(cur);
pour (int dir = 0; dir < 4; ++ dir) {
Int ni = cur[0] + dx[dir];
int nj = cur[1] + dy[dir];
si (ni >= 0 && ni < m && nj >= 0 && nj < n &&
[nj] == 1 & & & !vis[nj]] {
st.push(nouvelle int[]{ni, nj});
vis[ni][nj] = vrai;
}
}
}

// Normaliser les coordonnées par rapport à la première cellule
Int baseX = island.get(0)[0];
base intY = île.get(0)[1];
Liste<int[]> rel = nouvelle liste de distribution<>();
pour (int[] p : île) {
rel.add(nouvelle int[]{p[0] - baseX, p[1] - baseY});
}

// Générer une forme canonique
Chaîne canonique = canoniqueForm(rel);
voir.add (canonique);
}
}
}
retour vu.size();
}

Forme canonique à chaîne privée(Liste de forme <int[]>) {
Liste des formulaires <String> = nouvelle liste <>(8);
pour (int t = 0; t < 8; ++t) {
Liste<int[]> transformée = nouvelle ArrayList<>(shape.size());
pour (int[] p : forme) {
int x = p[0], y = p[1];
int nx = x, ny = y;
commutateur (t) {
cas 0: nx = x; ny = y; rupture; // 0°
cas 1: nx = -y; ny = x; rupture; // 90°
cas 2: nx = -x; ny = -y; rupture; // 180°
cas 3: nx = y; ny = -x; rupture; // 270°
cas 4: nx = x; ny = -y; rupture; // réflexion
cas 5: nx = -x; ny = y; rupture; // réflexion + 90°
cas 6: nx = -x; ny = -y; rupture; // réflexion + 180°
Cas 7: nx = y; ny = x; rupture; // réflexion + 270°
}
transformation.add(nouvelle int[]{nx, ny});
}
// Déplacement vers l ' origine
int minX = entier.MAX_VALUE, minY = entier.MAX_VALUE;
pour (int[] p : transformé) {
minX = Math.min(minX, p[0]);
minY = Math.min(minY, p[1]);
}
pour (int[] p : transformé) {
p[0] -= minX;
p[1] -= minY;
}
// Tri
(comparateur.comparantInt((int[] p) -> p[0)]
.thenComparingInt(p -> p[1]);
// Sérialiser
StringBuilder sb = nouveau StringBuilder();
pour (int[] p : transformé) {
sb.append(p[0]).append(',').append(p[1]).append(');
}
formulaires.add(sb.àString());
}
Collections.sort(formulaires);
retourner forms.get(0); // plus petite chaîne canonique
}
}
«» "

---

#### 5.2 Python 3

'`python
de taper l'importation Liste, jeu, tuple
à partir de collections import deque

Solution de classe:
def numDistinct Îles2(soi-même, grille: Liste[Liste[int]]) -> Int:
m, n = len(grid), len(grid[0])
vis = [[Faux] * n pour _ dans la plage(m)]
vu: Set[str] = set()

dirs = [(1, 0), (-1, 0), (0, 1), (0, -1)]

pour i dans la plage (m):
pour j dans la plage(n):
si grille[i][j]] 1 et non vis[i][j]:
# BFS / DFS
cellules: Liste[Tuple[int, int]] = []
dq = deque([i, j)]
vis[i][j] = Vrai
alors que dq:
x, y = dq.popleft()
(x, y))
pour dx, dy en dirs:
nx, ny = x + dx, y + dy
Si 0 <= nx < m et 0 <= ny < n et grille[nx]]] 1 et non vis[nx][ny]:
(nx, ny)
vis[nx][ny] = Vrai

# normaliser les coordonnées par rapport à la première cellule
base = cellules[0]
rel = [(x - base[0], y - base[1]) pour x, y dans les cellules]

canonique = self.canonical_form(rel)
voir.add(canonique)

retour len(see)

@staticmethod
def canonical_form(shape: List[Tuple[int, int]]) -> str:
formulaires = []
pour t dans la plage(8):
trans = []
pour x, y en forme:
si t == 0: nx, ny = x, y
* 1: nx, ny = -y, x
* 2: nx, ny = -x, -y
élif t == 3: nx, ny = y, -x
elif t == 4: nx, ny = x, -y
* 5: nx, ny = -y, -x
elif t == 6: nx, ny = -x, y
autres: nx, ny = y, x
(nx, ny)

# passage à l'origine
min_x = min(p[0] pour p en trans)
min_y = min(p[1] pour p en trans)
trans = [(p[0] - min_x, p[1] - min_y) pour p in trans]
Trans.sort()
formulaire.annexe(tuple(trans))

# Le plus petit tuple lexicographique est la clé canonique
retour str(min(forms))
«» "

---

Numéro 5.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int numDistinctIslands2(vecteur<vecteur<int>>& grille) {
int m = quadrillage(), n = quadrillage[0].size();
vecteur<vector<int>> vis(m, vecteur<int>(n, 0));
unordered_set<string> vu;
const int dx[4] = {1, -1, 0, 0};
const int dy[4] = {0, 0, 1, -1};

pour (int i = 0; i < m; ++i) {
pour (int j = 0; j < n; ++j) {
si (grid[i][j]== 1 && !vis[i][j]) {
vecteur<pair<int,int>> cellules;
file d'attente <pair<int,int>> q;
q.push({i, j});
vis[i][j] = 1;
pendant que (!q.vide()) {
auto [x, y] = q.front(); q.pop();
cells.push_back({x, y});
pour (int d = 0; d < 4; ++d) {
int nx = x + dx[d], ny = y + dy[d];
Si (nx >= 0 && nx < m && ny >= 0 && ny < n &&
1 &&!vis[nx][ny]) {
q.push({nx, ny});
[nx][ny] = 1;
}
}
}

// Coords relatifs
base int X = cellules[0].Premièrement, baseY = cellules[0]. deuxième;
vecteur<pair<int,int>> rel;
pour (auto &p : cellules)
rel.push_back({p.first - baseX, p.second - baseY});

chanoine = canonique Formulaire(rel);
voir.insérer(canon);
}
}
}
retour vu.size();
}

particulier:
chaîne canonique Forme(vecteur continu<pair<int,int>>&forme) {
forme vectorielle <string>;
pour (int t = 0; t < 8; ++t) {
vecteur<pair<int,int>> trans;
pour (auto &p : forme) {
int x = p.first, y = p.second;
La présente directive entre en vigueur le jour suivant celui de sa publication au Journal officiel de l'Union européenne.
commutateur (t) {
cas 0: nx = x; ny = y; rupture;
cas 1: nx = -y; ny = x; rupture;
cas 2: nx = -x; ny = -y; rupture;
cas 3: nx = y; ny = -x; rupture;
cas 4: nx = x; ny = -y; rupture;
cas 5: nx = -y; ny = -x; rupture;
cas 6: nx = -x; ny = y; rupture;
par défaut:nx = y; ny = x; break;
}
le nom de l'autorité compétente,
}

// Déplacement vers l ' origine
int minX = INT_MAX, minY = INT_MAX;
pour (auto &p : trans) {
minX = min(minX, p. premier);
minY = min(minY, p.seconde);
}
pour (auto &p : trans) {
p.premier -= minX;
p.seconde -= minY;
}

tri(trans.begin(), trans.end());
clé de chaîne;
pour (auto &p : trans) {
key += to_string(p.first) + ", + to_string(p.second) + ";
}
forms.push_back(key);
}
tri(forms.begin(), forms.end());
retourner les formulaires[0]; // chaîne minimale
}
};
«» "

---

<un nom="complexité"></a>## 6. Analyse de la complexité

Étape Complexe Raison
C'est quoi, ça ?
DFS par île **O(k)**="k" est le nombre de cellules dans cette île. Autres
8 transformations et normalisation **O(k log k)**= Tri de la liste des points (`k` <= zone de l'île). Autres
Autres Total pour toutes les îles **O(MN + K log K)** Pour les contraintes (`M,N <= 30`) c'est trivial. Autres

L'utilisation de l'espace est dominée par le tableau `visited` (`O(MN)`) et par l'ensemble de chaînes canoniques (`O(K)`), où `K` est le nombre total de cellules terrestres.

---

<un nom "test"></a>## 6. Conseils pour les essais

Scénario Résultat prévu
-- -- -- -- -- -- -- --
Exemple 1 (`grid = [[1,1,0],[1,1,0],[0,0]]') - Oui.
Exemple 2 (`grid = [[1,1,0,0],[1,0,0,0],[0,0,0,1],[0,0,0,1]) D'après les données
Autres Tous les zéros
Autres Une grande île en forme de carré
Autres Deux îles identiques séparées par l'eau
Autres Deux îles qui sont des reflets l'une de l'autre
Autres Deux îles qui diffèrent seulement par rotation

Exécutez chaque solution sur les entrées de l'échantillon; elles produisent toutes les sorties correctes.

---

<un nom="conclusion"></a>## 7. Pensées finales

* ** L'équivalence sous rotation et réflexion** peut être réduite à une chaîne **canonique** – c'est l'idée clé qui maintient l'algorithme rapide et précis.
* L'ensemble de transformation est petit (seulement 8), de sorte que nous pouvons nous permettre de les générer tous pour chaque île.
* La solution est ** entièrement déterministe**: deux îles équivalentes seront toujours map à la même clé exacte.
* Le code est **O(M·N)** dans le temps et **O(M·N)** dans l'espace, confortablement dans les limites des trois langues.

N'hésitez pas à copier l'extrait, à le coller dans votre IDE préféré, et à l'exécuter contre le problème LeetCode. Bon codage !

---

<un nom=faq></a>## 8. FAQ et pièges communs

Question Réponse
C'est pas vrai.
Autres **Pourquoi est-ce qu'on passe à l'origine après chaque transformation?**=Le déplacement supprime la position absolue; on se soucie seulement de la forme. Autres
Autres **Pouvons-nous sauter le décalage relatif si nous normalisons différemment?**=Vous devez changer; sinon deux îles qui se traduisent les unes des autres produisent des cordes différentes. Autres
Autres **Pourquoi choisir la plus petite corde comme forme canonique?** L'ordre lexicographique est déterministe et garantit l'unicité de toutes les transformations équivalentes. Autres
Avec `m,n <= 30`, la récursion est sûre, mais la DFS/BFS itérative est plus sûre pour les grandes grilles. Autres
Autres **Dons-nous stocker la coordonnée de base?** ► Nous n'en avons besoin que pour les coordonnées initiales relatives; après cela, toutes les transformations utilisent des coordonnées relatives. Autres

---

- Oui. 9. Mot final

Si vous vous préparez à des interviews ou à des concours de programmation concurrentiels, maîtriser ce modèle – ** produire des formes canoniques via des transformations** – sera inestimable.
Utilisez les extraits de code ci-dessus comme modèle pour les problèmes futurs qui impliquent l'équivalence de forme dans les opérations de symétrie.

Bon codage, et bonne chance avec LeetCode! C'est ce qu'il a dit.

---


> **Mots clés** – *Code Leet, Îles distinctes II, Java, Python, C++, forme canonique, rotations, réflexions, transformations, traversée de grille, algorithme *
> **Tags** – *LeetCode, Iles distinctes II, Array 2D, Forme canonique, Transformations, Codage Interview, Algorithmes*
---
> **Disclaimer** – Le code est fourni comme suit et n'a pas fait l'objet d'un test d'unité sur tous les cas bord.
> Veuillez adapter les directives de style à vos propres normes de codage.