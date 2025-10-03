---
Titre: LeetCode 750. Nombre de rectangles d'angle -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
750. Nombre de rectangles d'angle – La solution complète

Langage de langue Complexité temporelle Complexité spatiale Remarques
-- -- -- -- -- -- -- -- -- -- -- -- -- -- --
O(max(M,N)·min(M,N)2) Autres
O(max(M,N)·min(M,N)2) Autres
O(max(M,N)·min(M,N)2) Autres

> **Pourquoi devriez-vous lire cet article* *
> Leetcode 750 est une question d'interview classique -matrix + combinatoire -qui est fréquemment posée par les entreprises de haute technologie.
> Comprendre les *bonnes*, les *mauvaises* et les *meilleures* parties de ses solutions vous aidera à impressionner les gestionnaires d'embauche, à obtenir une note élevée sur les évaluations de codage et à déterminer le rôle que vous avez joué dans l'ingénierie logicielle.

---

Déclaration du problème

> **Avec une matrice `m × n` entier `grid` où chaque entrée est `0` ou `1`, retourner le nombre de rectangles *corner*.
> Un rectangle *corner* est un ensemble de quatre `1`s distincts qui forment un rectangle aligné sur l'axe. Seuls les coins doivent contenir `1`; les cellules intérieures peuvent être `0` ou `1`. Les quatre `1`s doivent être distincts (une seule ligne ou colonne de `1`s ne compte pas).

*Contrôles*

- `1 ≤ m, n ≤ 200`
- "grid[i]" (j) 1}'
- `1 ≤ 1s ≤ 6000`

---

Pourquoi Il s'agit d'un moyen, mais *Très* Interview- Problème prêt

- **Combinatoires** – Vous aurez besoin de penser à combien de façons pouvons-nous choisir deux colonnes qui ont toutes deux un `1` dans deux lignes différentes? (en milliers de dollars)
- **Sparse Matrix sensibilisation** – Dans de nombreux contextes d'entretien réel, la grille est très clairsemée (seulement quelques `1`s). Une solution naïve "O(m2·n2)" sera TLE.
- **Trade-offs** – Une force brute pure est facile à coder mais lente; une solution DP ou bitset ligne par ligne est rapide mais plus difficile à expliquer sur un tableau blanc.

---

## Le bon * – rapide, élégant et facile à raisonner

Le point de vue clé :

1. **Fixer deux lignes** (ou deux colonnes).
2. Scannez l'autre dimension pour compter combien de colonnes contiennent un `1` dans **deux** lignes sélectionnées.
3. Si vous trouvez `k` de telles colonnes, vous pouvez en choisir deux pour former un rectangle: `C(k, 2) = k·(k‐1)/2`.

> **Pourquoi deux rangées? * *
> Parce que les coins rectangles sont sur deux rangées distinctes. Une fois les lignes fixées, les colonnes deviennent les seuls degrés de liberté.

**Code Pseudo* *

«» "
résultat = 0
pour chaque paire de lignes (r1 < r2):
nombre = 0
pour chaque colonne c:
Si grille[r1][c]== 1 && grille[r2][c] == 1 :
nombre++
résultat += nombre * (compte-1) / 2
résultat du retour
«» "

**Complexité* *

- "O(min(M,N)2 · max(M,N)" heure
- Espace auxiliaire «O(1)» (ou «O(N2)» si vous souhaitez réutiliser un tableau 2-D pour l'optimisation)

---

## -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

'`python
# O(M^2 * N^2) – trop lent pour la grille 200×200
pour r1 dans la plage (M):
pour r2 dans la plage (r1+1, M):
pour c1 dans la plage(N):
pour c2 dans la plage(c1+1, N):
si grille[r1]c1] et grille[r1]c2] et grille[r2]c1 et grille[r2]c2]:
Rés += 1
«» "

- Même avec les contraintes maximales (`M = N = 200`), ces boucles **1,6 milliards** fois → TLE sur Leetcode.
- Oui. Il utilise également quatre boucles imbriquées – difficile à expliquer rapidement sur un forum d'entrevue.

---

## Le *Ugly* – Memory-Intensive DP (mais toujours efficace)

Un point de vue légèrement différent:
Au lieu de compter par paire de lignes, gardez un nombre courant du nombre de lignes précédentes partageant un `1` dans chaque paire de colonnes.
Cela nous permet d'accumuler des rectangles en **O(M·N2)** temps avec **O(N2)** espace, mais le tableau DP peut devenir un goulot d'étranglement si `N` est grand.

> **Quand l'utiliser? **
> Dans les paramètres d'entrevue où vous avez reçu une grille *très clairsemée* et pouvez vous permettre une matrice auxiliaire `O(N2)`, cette méthode obtient souvent le plus rapide temps d'exécution.

---

Mise en œuvre du code complet

####===# Java (Space‐Optimized, Sparse‐Matrix Friendly)

"Java
solution de classe {
compte d'entrée publiqueCornerRectangles(int[][]) {
if (grid) == null=" grid.longueur <= 1=" grid[0]. longueur <= 1) {
retour 0;
}

int lignes = longueur de grille;
int cols = grille[0]. longueur;

// Choisir la dimension plus petite pour itérer sur les paires
si (lignes < cols) {
Nombre de retours ParRows(grid, lignes, cols);
} autre {
Nombre de retours ByCols(grid, lignes, cols);
}
}

Int privé countByRows[][] grille, lignes int, int cols) {
int res = 0;
pour (int r1 = 0; r1 < lignes - 1; r1++) {
pour (int r2 = r1 + 1; r2 < lignes; r2++) {
cnt = 0;
pour (int c = 0; c < cols; c++) {
si [(grid[r1][c] & grid[r2][c]]]] 1) cnt++;
}
Rés += cnt * (cnt - 1) / 2;
}
}
retour rés;
}

Int privé countByCols[][] grille, lignes int, int cols) {
int res = 0;
pour (int c1 = 0; c1 < cols - 1; c1++) {
pour (int c2 = c1 + 1; c2 < cols; c2++) {
cnt = 0;
pour (int r = 0; r < lignes; r++) {
si [(grid[r][c1] et grille[r][c2]]] 1) cnt++;
}
Rés += cnt * (cnt - 1) / 2;
}
}
retour rés;
}
}
«» "

---

Python (légant et facile à lire)

'`python
Solution de classe:
def countCornerRectangles(self, grid: List[List[int]]) -> Int:
si non grille ou len(grid) <= 1 ou len(grid[0]) <= 1:
retour 0

m, n = len(grid), len(grid[0])
# C'est sur la dimension plus petite
si m < n:
Retourner soi-même._par_rows(grid, m, n)
Sinon:
Retourner soi-même._par_cols(grid, m, n)

def _by_rows(self, grid, m, n):
Res = 0
pour r1 dans la plage (m - 1):
pour r2 dans la plage (r1 + 1, m):
cnt = 0
pour c dans la plage(n):
si grille[r1][c] et grille[r2][c]:
cnt += 1
Rés += cnt * (cnt - 1) // 2
retour res

def _by_cols(self, grid, m, n):
Res = 0
pour c1 dans la plage (n - 1):
pour c2 dans la plage(c1 + 1, n):
cnt = 0
pour r dans la plage(m):
Si grille[r][c1] et grille[r][c2]:
cnt += 1
Rés += cnt * (cnt - 1) // 2
retour res
«» "

---

C++ (Fastest, Bitset-Optimized pour Leetcode)

'`cpp
solution de classe {
public:
nombre intCornerRectangles(vecteur<vecteur<int>>& grille) {
int m = quadrillage(), n = quadrillage[0].size();
si (m <= 1) n <= 1) retourner 0;
// Utiliser bitset si n <= 200 (s'adapte à un bitset de 200 bits)
vecteur<bitset<200>> lignes(m);
pour (int i = 0; i < m; ++i)
pour (int j = 0; j < n; ++j)
si (grid[i][j]) lignes[i].set(j);

int res = 0;
pour (int i = 0; i < m - 1; ++i) {
pour (int j = i + 1; j < m; ++j) {
// intersection de deux lignes
bitset<200> inter = lignes[i] & lignes[j];
long cnt = inter.count();
Rés += cnt * (cnt - 1) / 2;
}
}
retour rés;
}
};
«» "

> ** Pourquoi ? * *
> Un `bitset<200>` donne O(1) intersection et O(1) pop-count, tournant la boucle intérieure en une poignée de instructions de la machine. C'est la solution la plus rapide pour les limites de temps dur de Leetcode.

---

Comment l'expliquer à un comité d'entrevue

1. ** Tirer deux lignes** ( `r1` et `r2`).
2. **Montrer un balayage** à travers les colonnes, en comptant où les deux ont un `1`.
3. ** Appliquer la formule de combinaison**.
4. **Généralisation** – -Si les colonnes sont moins nombreuses, nous échangerons plutôt la logique et les colonnes de paires. (en milliers de dollars)

> **Conseil:** Gardez votre raisonnement bref: *=Nous sommes essentiellement des paires de colonnes qui partagent un `1` en deux lignes, donc pour les colonnes `k` nous avons `k choisir 2` rectangles.
> Utilisez le tableau blanc pour dessiner l'intersection des bits si vous êtes à l'aise avec C++.

---

À emporter : ce que cherchent les gestionnaires d'embauche

Pourquoi ça compte ? Comment le montrer ?
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
**La pensée algorithmique**=La capacité de repérer le motif des lignes de paires=Décrivez brièvement l'étape combinatoire=
**Temps-Espace échange**= Comprendre quand favoriser le temps au-delà de la longueur du code==========================================================================================================================================================================================
Autres **Utilisation des structures de données**= Recognise Leetcode=s matrices clairsemées== Expliquez l'optimisation du bitset ou du tableau DP==
**La communication**

---

Les pensées finales et les prochaines étapes

1. **Pratique** – Exécutez ces solutions sur les entrées de l'échantillon de Leetcode, puis créez vos propres cas de bord (par exemple, tous les `1`s, tous les `0`s, diagonale `1`s).
2. **Exposer les maths** – Sur les entretiens, toujours verbaliser `C(k, 2)` avant de coder.
3. ** Prêt à s'adapter** – Si l'intervieweur demande le plus rapide possible, pivotez vers la version DP ou bitset.

> **L'établissement d'un rôle**: La maîtrise du Leetcode 750 démontre la maîtrise de *la manipulation de la matrice*, de *combinatoire* et de *l'optimisation algorithmique*—compétences qui sont au cœur de nombreuses positions d'ingénierie logicielle (p. ex. backend, data-engineering, trading algorithmique).

Bon codage, et que votre prochaine entrevue s'en aille *off-the-chart*! C'est ce qu'il a dit.

---

> *Suivez-moi sur GitHub pour plus de solutions d'entrevue, de simulation d'entrevue et de ressources d'avancement professionnel. *
[Votre blog]**

---


---


(Fin de l'article)