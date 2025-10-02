---
titre: LeetCode 3128. Triangles droit - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Solutions en trois langues pour LeetCode 3128 – * Triangles de droite*

Ci-dessous sont des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++** qui résolvent le problème dans *O(m × n*) et *O(m + n*) une mémoire supplémentaire, où *m* est le nombre de lignes et *n* le nombre de colonnes.

> **Récapitulation des problèmes**
> Un triangle droit** est formé par trois cellules qui contiennent toutes «1».
> Un vertex doit partager un **row** avec le deuxième vertex, et le premier vertex doit partager un **colonne** avec le troisième vertex.
> Comptez tous ces triangles dans une matrice binaire.

---

#### 1.1 Java

"Java
Importation de java.util.*;

solution de classe {
nombre public longOfRightTriangles(int[][]) {
int lignes = longueur de grille;
int cols = grille[0]. longueur;

// Précompter ceux de chaque ligne et colonne
int[] rowCnt = nouveau int[rows];
int[] colCnt = nouveau int[cols];

pour (int r = 0; r < lignes; r++) {
pour (int c = 0; c < cols; c++) {
si [grid[r][c]] 1) {
ligne Cnt[r]++;
pour les véhicules automobiles
}
}
}

triangles longs = 0;
pour (int r = 0; r < lignes; r++) {
pour (int c = 0; c < cols; c++) {
si [grid[r][c]] 1) {
// (rowCnt[r] - 1) choix pour la jambe horizontale
// (colCnt[c] - 1) choix pour la jambe verticale
triangles += 1L * (rowCnt[r] - 1) * (colCnt[c] - 1);
}
}
}
triangles de retour;
}
}
«» "

*Pourquoi "long"? *
Le nombre maximal de triangles peut atteindre `1012` (1 000 × 1 000 quadrillage rempli de ceux-ci). "int" déborderait.

---

#### 1.2 Python

'`python
Solution de classe:
Numéro DeRightTriangles(même, grille: Liste[Liste[int]]) -> Int:
rangées, cols = len(grid), len(grid[0])

# Compteurs de lignes et de colonnes
ligne_cnt = [0] * lignes
col_cnt = [0] * cols

pour r dans la plage (lignes):
pour c dans la plage(cols):
si grille[r][c]:
ligne_cnt[r] += 1
_cnt[c] += 1

triangles = 0
pour r dans la plage (lignes):
pour c dans la plage(cols):
si grille[r][c]:
triangles += (row_cnt[r] - 1) * (col_cnt[c] - 1)

triangles de retour
«» "

Les entiers de précision arbitraire de Python signifient que nous n'avons pas besoin de nous inquiéter du débordement.

---

*## 1.3 C++

'`cpp
#incluez <vecteur>

solution de classe {
public:
long long nombreOfRightTriangles(std::vector<std::vector<int>>& grille) {
lignes int = grille.size();
int cols = grille[0].taille();

std:vector<int> rangCnt(lignes, 0), colCnt(cols, 0);

// Nombre 1 dans chaque rangée et colonne
pour (int r = 0; r < lignes; ++r)
pour (int c = 0; c < cols; ++c)
si [grid[r][c]] {
++Cnt[r];
+colCnt[c];
}

triangles longs = 0;
pour (int r = 0; r < lignes; ++r)
pour (int c = 0; c < cols; ++c)
si [grid[r][c]] {
triangles += 1LL * (rowCnt[r] - 1) * (colCnt[c] - 1);
}

triangles de retour;
}
};
«» "

"long long" garantit un arithmétique 64 bits sûr.

---

- Oui. 2. Article de blog: -Le bon, le mauvais, et l'acharnement de compter les triangles droit

2.1 Pourquoi ce problème compte dans les entrevues

- **Matrix traversal** – une base de questions d'entrevue.
- **Combinaison de comptage** – testez si vous pouvez repérer des solutions *O(m × n)* au lieu de la force brute O(m × n)3).
- **La pensée d'Edge-case** – gérer de très grandes sorties et contraintes de mémoire.
- **Mauvaise maîtrise de la langue** – les intervieweurs demandent souvent des solutions Java/Python/C++ à la volée.

2.2 Le bon – Intuition et simplicité

Le point de vue clé :
> *Si une cellule (r, c) est un vertex à angle droit, tout autre `1` dans sa rangée peut être la jambe horizontale, et tout autre `1` dans sa colonne peut être la jambe verticale. *

Ainsi, pour chaque `1` nous n'avons besoin que des nombres de `1` dans sa ligne et sa colonne.
Le nombre de triangles avec cette cellule comme angle droit est simplement
«(rowCount[r] – 1) × (colCount[c] – 1)».

Cela réduit une explosion apparemment combinatoire à un passage linéaire.

2.3 Les mauvaises – approches naïves qui TLE

A simple O((m × n)3) un algorithme :
1. Énumérer tous les triplets de cellules.
2. Vérifiez l'état géométrique.

Même pour une grille 100×100, cela implique des milliards d'opérations, bien au-delà des limites de temps d'entrevue.
Les contraintes du problème (1000×1000) excluent toute solution cubique ou quadratique en cellules.

#### 2.4 Le mauvais – Coin Cases & Overflow

- **Toutes les cellules sont "1"**:
Le nombre de triangles peut être aussi élevé que
(LowCount[r] – 1) × (colCount[c] – 1)`
Utiliser des débordements entiers de 32 bits; utiliser 64 bits (long'/long').
- ** Grilles de séparation** :
De nombreuses lignes/colonnes contiennent zéro `1`s. Notre algorithme gère cela gracieusement parce que `(rowCount[r] – 1)` devient négatif seulement si `rowCount[r] == 0`, mais nous veillons en vérifiant `grid[r][c] == 1' avant le calcul du produit.
- **Inputs non rectangulaires**:
LeetCode garantit `grid[i].length` est constant, mais le code défensif peut affirmer ou gérer des tableaux déchiffrés.

#### 2.5 Étape par étape (Java)

Texte
1. Compter 1s dans chaque rangée → rowCnt[]
2. Compte 1 dans chaque colonne → colCnt[]
3. Pour chaque cellule qui est 1:
triangles += (rowCnt[r] - 1) * (colCnt[c] - 1)
«» "

Les deux premiers passages sont O(m × n).
La troisième passe est également O(m × n).
Durée totale: **O(m × n)**.
Mémoire supplémentaire : **O(m + n)** pour les compteurs.

2.6 Analyse de la complexité

Opération Temps Espace
- C'est quoi ?
Autres Nombre de lignes O(m × n)
Autres Colonnes de comptage
Calcul des triangles O(m × n) O(1) (à l'exception des compteurs)
Total**************************

Cela répond confortablement aux contraintes:
- Pour une grille 1000 × 1000 : ~1 000 000 opérations, ~8 KB de stockage auxiliaire.

2.7 Essais et bords Liste de contrôle des cas

Autres Test de la grille Prévue Raison
- C'est quoi ?
Tous les zéros 3×3 tous `0`
Autres Tous les nombres: 4×4 tous les nombres: 4 * (3 * 3) = 36
Autres 3×3 avec isolé `1`-0' Besoin d'au moins deux 1s dans la même rangée/col
2×5 grille de calcul Compter en conséquence
Autres Grande entrée : 1000×1000 avec 50% d'entre eux.

### 2.8 A emporter pour votre prochaine entrevue

- ** Commencez par compter les aides** : Lorsqu'un problème implique des contraintes de même ligne / même colonne, pré-calculez les fréquences de ligne / colonne.
- ** Méfiez-vous des débordements entiers**: Si vous soupçonnez que les résultats peuvent dépasser 231 – 1, utilisez des types 64 bits.
- ** Expliquez votre logique** : Même si votre code est parfait, articuler l'intuition (comme la vue du vertex d'angle droit) impressionne les intervieweurs.
- **La complexité du temps d'abord**: Montrez que vous avez considéré O((m × n)3) et pourquoi il échoue avant de présenter la solution O(m × n).

2.9 Verdict final

- **Bonne** – Un bel algorithme *O(m × n)* qui est à la fois **efficace** et **readable**.
- **Bad** – Toute approche de force brute *time-out* sur de grands cas d'essai.
- **Ugly** – Attention au débordement et à la sparsité, mais un produit 64-bit soigné le corrige.

Ce problème est un exemple *classique* de la façon dont une simple observation combinatoire peut transformer un défi apparemment insoluble en une solution propre et conviviale. La maîtriser vous donnera une base solide pour toute question d'entrevue basée sur une matrice.

---

2.9 Vous voulez impressionner encore plus?

- **Ajouter un liner pour Python** :
'`python
triangles = somme((row_cnt[r]-1)*(col_cnt[c]-1)
pour r dans l'intervalle (lignes) pour c dans l'intervalle (cols) si grille[r][c])
«» "
- **Parallélisation des discussions**: Deux scans distincts peuvent être exécutés en parallèle; parlez de la possibilité si l'intervieweur demande au sujet de *distributed computing*.

2.10 Mot final

Compter les triangles de droite est un microcosme du thème d'entrevue *-Matrix + combinatoire + comptage soigneux. En apprenant le modèle du calcul du vertex de l'angle droit, vous serez prêt pour une grande variété de questions d'entrevue qui vous demandent de *compter* structures à l'intérieur des grilles 2-D.

Bon codage – et bonne chance pour votre prochaine entrevue!