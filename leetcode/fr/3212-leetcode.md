---
Titre: LeetCode 3212. Sous-matrices de dénombrement Avec une fréquence égale de X et Y -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Problème 3212 – Sous-matrices de compte Avec une fréquence égale de X et Y

* **Source**: LeetCode 3212
* **Input**: `grid[r][c]` où chaque cellule contient une de `{'X','Y','.'}`.
* **Objectif**: Compter **tous** sous-matrices qui **départent au coin supérieur gauche (0, 0)** et dont le nombre de cellules `X` est égal au nombre de cellules `Y` **et** contiennent au moins une `X`.
* **Constances**: "1 ≤ r, c ≤ 1000".

La déclaration originale peut sonner comme un problème typique de nombre de rectangles, mais les exemples montrent clairement que nous ne nous soucions que des rectangles qui commencent à l'origine.

---

- Oui. 2. La bonne idée de base

L'exigence selon laquelle chaque rectangle compté commence à `(0,0)` transforme l'ensemble du problème en un exercice préfixe très simple.

* **Préfixe de X**
`preX[i+1][j+1]` = nombre de `X` dans le rectangle `(0,0) ... (i,j)`.
* **Préfixe de Y**
`preY[i+1][j+1]` = nombre de `Y` dans le même rectangle.

Si `preX[i+1][j+1] == preY[i+1][j+1]` et que la valeur est **positive**, alors le sous-matrix `(0,0) ... (i,j)` remplit les deux conditions: nombres égaux de `X` et `Y`, et au moins un `X`.

Il nous suffit donc d'une boucle imbriquée sur toutes les cellules, pour vérifier cette égalité.

---

- Oui. 3. Les pièges communs

Pourquoi il échoue Comment éviter
C'est pas vrai.
**En supposant qu'il faut compter chaque rectangle**L'exemple avec `X X / X Y` a un sous-matrice de 2 colonnes `(0,1)-(1,1)` qui satisferait l'égalité, mais la réponse est `0`. Prêtez une attention particulière à l'énoncé – seules les sous-matrices `(0,0)'–origine sont comptées. Autres
**L'utilisation d'un tableau 3-D ou "long" pour le préfixe**.La mémoire inutile, un accès plus lent. Autres
**Le calcul de tous les rectangles égaux – X/Y – dépasserait les rectangles qui ne contiennent que des cellules `.`. 0` avant d'augmenter la réponse. Autres
**Les erreurs d'indexation basées sur les zéros et les uns**Les bogues off-by-one qui produisent des nombres incorrects. Construire des tableaux préfixes avec une rangée/colonne supplémentaire de zéros (`size = r+1, c+1`) pour éviter les vérifications. Autres

---

- Oui. 4. L'Ugly – Comment le rendre rapide et mémoire‐ Amiable

Bien que la double boucle naïve soit déjà `O(r·c)`, vous pouvez serrer la mémoire:

1. **Restaurer seulement la ligne actuelle des montants préfixés** –
Conservez deux tableaux 1-D `cntX[c]` et `cntY[c]` et mettez-les à jour en scannant chaque ligne.
Après traitement de la ligne `i`, `cntX[j]` détient le total `X` dans la colonne `j` de la ligne 0 à la ligne i.
Un rectangle se terminant à `(i,j)` satisfait à la condition sif `cntX[j] == cntY[j]` ** et** "cntX[j] > 0".
Cela utilise la mémoire supplémentaire "O(c)` au lieu de "O(r·c)".

2. **Éviter le débordement entier** –
Dans la version préfixe 2D, le nombre maximal est `1000·1000 = 106`, bien au-dessous `INT_MAX`.
Si vous comptiez tous les rectangles (pas le problème original de LeetCode), vous auriez besoin d'un `long`.

---

- Oui. 5. Code final

Ci-dessous vous trouverez des solutions propres et prêtes à la production pour **Java**, **Python** et **C++**.
Tous les trois partagent la même logique algorithmique – calculez les montants du préfixe pour `X` et `Y`, puis scannez la grille.

---

Oui. Java

"Java
// LeetCode 3212 – Sous-matrices de comptage Avec une fréquence égale de X et de Y
// À partir de (0,0) seulement

Importation de java.util.*;

solution de classe {
numéro int public OfSubmatrices(char[]]) {
int lignes = longueur de grille;
int cols = grille[0]. longueur;

// Préfixer les sommes: preX[i+1][j+1] = #X dans le rectangle (0,0)-(i,j)
int[] preX = nouvelle int[lignes + 1][cols + 1];
int[] preY = nouvelle int[lignes + 1][cols + 1];

pour (int i = 0; i < lignes; ++i) {
pour (int j = 0; j < cols; ++j) {
preX[i + 1][j + 1] = preX[i][j + 1] + preX[i + 1][j] - preX[i][j]
+ (grid[i][j] == 'X' ? 1 : 0);
preY[i + 1][j + 1] = preY[i][j + 1] + preY[i + 1][j] - preY[i][j]
+ (grid[i][j] == 'Y' ? 1 : 0);
}
}

Int ans = 0;
pour (int i = 0; i < lignes; ++i) {
pour (int j = 0; j < cols; ++j) {
int xCnt = preX[i + 1][j + 1];
int yCnt = preY[i + 1][j + 1];
si (xCnt > 0 && xCnt == yCnt) {
as++;
}
}
}
le retour des an;
}
}
«» "

---

5.2. Python 3

'`python
# LeetCode 3212 – Sous-matrices de comptage Avec une fréquence égale de X et de Y
# À partir de (0,0) seulement

def number_of_submatrices(grid: list[list[str]]) -> Int:
rangées, cols = len(grid), len(grid[0])

# préfixer les sommes pour X et Y
pre_x = [[0] * (cols + 1) pour _ dans l'intervalle (lignes + 1)]
pre_y = [[0] * (cols + 1) pour _ dans l'intervalle (lignes + 1)]

pour i dans la plage (lignes):
pour j dans la plage(cols):
pré_x[i + 1][j + 1] = (
Pré_x[i][j + 1] + pre_x[i + 1][j] - pre_x[i][j]
+ (1 si grille[i][j]] 'X' autre 0)
)
pré_y[i + 1][j + 1] = (
Pré_y[i][j + 1] + pré_y[i + 1][j] - pré_y[i][j]
+ (1 si grille[i][j]] 'Y' autre 0)
)

ans = 0
pour i dans la plage (lignes):
pour j dans la plage(cols):
Si pre_x[i + 1][j + 1] > 0 et pre_x[i + 1][j + 1]] == pre_y[i + 1][j + 1]:
+= 1
retour et
«» "

---

#### 5.3. C++

'`cpp
// LeetCode 3212 – Sous-matrices de comptage Avec une fréquence égale de X et de Y
// À partir de (0,0) seulement

#incluez <vecteur>
#incluez <string>

solution de classe {
public:
nombre intOfSubmatrices(const std::vector<std::string>& grille) {
Int R = quadrillage.size();
int C = grille[0].taille();

// Préfixer les sommes: preX[i+1][j+1] détient #X en rectangle (0,0)-(i,j)
(C + 1, 0));
std::vector<std::vector<int>> preY(R + 1, std::vector<int>(C + 1, 0));

pour (int i = 0; i < R; ++i) {
pour (int j = 0; j < C; ++j) {
preX[i + 1][j + 1] =
PréX[i][j + 1] + preX[i + 1][j] - preX[i][j]
+ (grid[i][j] == 'X' ? 1 : 0);
PréY[i + 1] [j + 1] =
PréY[i][j + 1] + preY[i + 1][j] - preY[i][j]
+ (grid[i][j] == 'Y' ? 1 : 0);
}
}

Int ans = 0;
pour (int i = 0; i < R; ++i) {
pour (int j = 0; j < C; ++j) {
int xCnt = preX[i + 1][j + 1];
int yCnt = preY[i + 1][j + 1];
si (xCnt > 0 && xCnt == yCnt) ++ans;
}
}
le retour des an;
}
};
«» "

---

- Oui. 6. Analyse de la complexité

Délai de mise en œuvre
- Oui.
Autres Préfixe 2-D (Java, Python, C++)="O(r · c)" (= 106 opérations pour le pire des cas)="O(r+1)(c+1)" entiers – ~ 8 Mo pour une grille 1000×1000
Variante 1-D-row-by-row (Java & C++)

Les deux respectent les limites de temps LeetCode confortablement.

---

- Oui. 7. Tester votre solution

'`python
si __nom__ == "__main__" :
échantillon = [
['.', 'X', 'X'],
['X', 'X', 'Y'],
['.', '.', 'Y']
- Oui.
print(number_of_submatrices(échantillon)) # Attendu: 4
«» "

Pour l'autre exemple qui démontre l'exigence «origin‐only» :

'`python
échantillon2 = [
['X', 'X'],
['X', 'Y']
- Oui.
print(nombre_de_sous-matrices(échantillon2)) # Prévu : 0
«» "

---

- Oui. 8. A emporter

* **Rappel**: Dans LeetCode 3212 les rectangles que nous comptons ** commencent toujours à (0, 0)**.
* La solution se résume à un parcours bidimensionnel préfixe.
* La clause "X" au moins est exécutée par une seule "> 0' vérification.
* Pour des économies de mémoire supplémentaires, vous ne pouvez garder qu'un compte de course unidimensionnel par colonne.

Avec les extraits de code ci-dessus, vous pouvez résoudre le problème en toute confiance en **Java, Python ou C++** et soumettre une solution propre et prête à la production à LeetCode. Bon codage !