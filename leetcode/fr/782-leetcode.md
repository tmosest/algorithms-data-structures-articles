---
titre: LeetCode 782. Transformer en Chessboard -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

La transformation en tableau d'échecs – LeetCode 782
### Les bons, les mauvais et les méchants – Un guide complet et optimisé pour le référencement

> **TL;DR** – En une seule ligne, vous pouvez transformer un tableau binaire en un échiquier en échangeant des lignes et des colonnes. L'astuce est de valider le modèle, compter les erreurs, fixer la parité, et diviser par deux.
>
> Complexité: **O(n2)** temps, **O(1)** espace auxiliaire.
>
> Code: **Java, Python, C++** – commentaire complet, prêt pour l'interview.

---

Table des matières

1. [Énoncé du problème] (#Énoncé du problème)
2. [Pourquoi c'est dur]
3. [Aperçu de la solution](#solution-overview)
* 1-vérification de la validité du passage
* Décompte des swaps pour lignes et colonnes
* Manipulation de tailles impairs ou égales
Réponse finale = (waps de lignes + colwaps) / 2
4. [Algorithme détaillé] (#algorithme détaillé)
5. [Proof of Correctness] (#proof of Correctness)
6. [Analyse de la complexité] (#analyse de la complexité)
7. [Régimes et pièges] (#cases--règles)
8. [Mise en œuvre de Java] (#Mise en œuvre de Java)
9. [Python implementation] (#python implementation)
10. [Mise en œuvre C++](#c-mise en œuvre)
11. [Testing & Sample Runs](#test--sample-runs)
12. [Traitement et conseils d'entrevue] (#tâche--entrevue-tâches)
13. [Mots de référence et métadonnées](#seo-keys)

---

- Oui. 1. Exposé des problèmes

> **LeetCode 782 – Transformer en tableau d'échecs* *
> **Difficulté**: dur
>
> Avec une grille binaire `n × n` `board`, vous pouvez échanger deux lignes ou deux colonnes n'importe quel nombre de fois.
> Retourner le nombre minimum de mouvements** requis pour transformer le tableau en un tableau de bord** (c.-à-d. qu'aucune cellule adjacente ne partage la même valeur). Si c'est impossible, retournez `-1`.

---

- Oui. 2. Pourquoi c'est dur

* **Constraint:** `n` ≤ 30 – assez petit pour un algorithme `O(n2)`, mais vous avez encore besoin d'un astuce de validation *linéaire-temps*.
* **Problème de rareté:** Même contre la taille du tableau impair change le nombre optimal de swaps.
* **Row/Colonne Symmetry:** Les lignes et colonnes sont indépendantes mais doivent satisfaire aux mêmes règles de faisabilité.
* **Trouver efficacement les swaps :** Vous ne pouvez pas simuler chaque échange ; vous avez besoin d'une formule basée sur des erreurs d'appariement.

---

- Oui. 3. Aperçu de la solution

1. ** Vérification de faisabilité* *
* Chaque cellule `(r, c)` doit satisfaire
"board[r][c] ==board[0][0] ^board[r][0] ^board[0][c]".
* Si une cellule viole cela, la carte ne peut pas être transformée → retourner `-1`.

2. **Mise en correspondance des lignes et des colonnes* *
* Pour les lignes : compter combien de lignes correspondent au motif `[0,1,0,1,...]`.
* Pour les colonnes: compter combien de colonnes correspondent au motif `[0,1,0,1,...]`.
* Calculez également `rowSwap` = nombre de lignes qui commencent déjà avec la parité correcte (c.-à-d. `board[r][0] == r % 2`).
* De même pour le colSwap.

3. ** Fréquences de validation**
* Le nombre de `1`s dans n'importe quelle ligne ou colonne doit être `=n/2=" ou `=n/2=".
* Sinon, la transformation est impossible.

4. **Découpes minimales de calcul**
* ** Même n:**
* `rowSwaps = min(rowSwap, n - rowSwap)`
* `colSwaps = min(colSwap, n - colSwap)`
* **Durée n:**
* La parité de départ doit correspondre à la majorité.
* Si `rowSwap` est impair → `rowSwap = n - rowSwap`
* De même pour le colSwap.

5. **Réponse**
* Chaque swap fixe deux positions, de sorte que le total des déplacements = `(rowSwaps + colSwaps) / 2`.

---

- Oui. 4. Algorithme détaillé (étape par étape)

«» "
n = longueur de la planche
ligneSum = colSum = 0
rowSwap = colSwap = 0

// 1. Contrôle de faisabilité
pour r dans 0..n-1:
pour c dans 0..n-1:
si [board[0][0] ^board[r][0] ^board[0][c] ^board[r]]]] 1 :
retour -1

// 2. Compter les lignes/cols qui sont "good" et les erreurs d'appariement
pour i en 0..n-1:
rowSum += planche[0][i] // nombre de 1s dans la première rangée
colSum += planche[i][0] // nombre de 1s dans la première colonne
rowSwap += (board[i][0]]. i%2) ? 1 : 0
(bord [0] [i]] i%2) ? 1 : 0

// 3. Valider un compte
si la ligneSum n'est pas [n/2, (n+1)/2] ou le colSum n'est pas [n/2, (n+1)/2]:
retour -1

// 4. Ajustement des swaps sur la base de la parité
Si n % 2 == 1: // taille du tableau impair
si rowSwap % 2 == 1: rowSwap = n - rowSwap
Si colSwap % 2 == 1: colSwap = n - colSwap
Autre: // même taille de la planche
rowSwap = min(rowSwap, n - rowSwap)
colSwap = min(colSwap, n - colSwap)

// 5. Retourner des mouvements minimes
retour (rowSwap + colSwap) / 2
«» "

---

- Oui. 5. Preuve d'exactitude

1. **Conditions de faisabilité**
* Pour deux lignes `r1, r2` et deux colonnes `c1, c2`, les quatre cellules `(r1, c1),(r1, c2),(r2, c1),(r2, c2)` doivent former un motif de tableau de bord.
* Algébrique, cela est équivalent à la condition XOR ci-dessus.
* Si le tableau échoue, aucune séquence d'échange ne peut corriger le motif.

2. **Compte de l ' échange entre la population et la population**
* Les lignes d'échange qui sont déjà dans le modèle désiré avec ceux qui sont , réduit les erreurs d'appariement par exactement un chacun.
* Le nombre minimal d'échanges pour faire alterner toutes les lignes est `min(rowSwap, n-rowSwap)` pour même `n`; pour impair `n`, la parité force une orientation exacte.

3. ** Division par deux**
* Un seul swap de deux lignes corrige deux positions (les deux lignes).
* De même pour les colonnes.
* Ainsi, le nombre total de mouvements équivaut à la moitié du nombre total d'erreurs.

L'algorithme suit les étapes logiques ci-dessus, garantissant des mouvements minimes si la carte est transformable.

---

- Oui. 6. Analyse de la complexité

* **Heure:**
* Vérification de faisabilité: `O(n2)`
* Boucles de comptage: `O(n)` (en fait `O(n)` pour chacune des deux passes, toujours `O(n)`)
* Dans l'ensemble : **O(n2)** (dominant par vérification de faisabilité)

* **Espace:**
* Seulement une poignée de compteurs entiers → **O(1)** espace auxiliaire.

Avec `n ≤ 30`, cela fonctionne en microsecondes sur n'importe quelle machine moderne.

---

- Oui. 7. Cas de bord et pièges

Qu'est-ce que regarder ?
- Oui.
La parité de "rowSwap"/"colSwap" doit être égale. Autres
**Le nombre de 1s doit être soit `n/2` ou `(n+1)/2`. Autres
Autres **Tous les zéros ou tous les zéros** Le contrôle XOR l'attrape. Autres
**Large n (30)** Pas besoin d'optimisation. Autres
**Enregistrement de la même ligne deux fois** Pas nécessaire, la formule la gère. Autres

---

- Oui. 8. Mise en œuvre de Java

"Java
***
* 782. Transformer en tableau d'échecs
*
* Solution Java qui fonctionne dans l'espace O(n^2).
* Implémente la stratégie optimale de comptage des swaps expliquée ci-dessus.
*/
solution de classe {
mouvement public d'inteToChessboard(int[[]]) {
int n = tableau. longueur;
dans la rangéeSum = 0, colSum = 0; // nombre de 1s dans la première rangée/colonne
int rowSwap = 0, colSwap = 0; // rows/cols déjà en bonne parité

- Oui. 1. Contrôle de faisabilité
pour (int r = 0; r < n; r++) {
pour (int c = 0; c < n; c++) {
// la planche[r][c] doit être égale à la planche[0][0] ^ la planche[r][0] ^ la planche[0][c]
si [((board[0]]0] ^board[r]0] ^board[0][c] ^board[r][c]] et 1)] 1) {
retour -1;
}
}
}

- Oui. 2. Compter les rangées/cols qui correspondent à --------- */
pour (int i = 0; i < n; i++) {
rowSum += planche[0][i]; // 1s dans la première rangée
colSum += planche[i][0]; // 1s dans la première colonne
si (board[i][0] == (i & 1)) rowSwap++; // row commence avec la parité correcte
si (board[0][i] == (i & 1)) colSwap++; // colonne commence avec la parité correcte
}

- Oui. 3. Valider 1 compte --------- */
si (rowSum < n / 2-) rowSum > (n + 1) / 2) retourner -1;
si (colSum < n / 2) colSum > (n + 1) / 2) retour -1;

- Oui. 4. Ajustement des swaps sur la base de la parité --------- */
si (n & 1)] 1) { // taille du panneau impair
si ((rowSwap & 1) == 1) rowSwap = n - rowSwap;
si ((colSwap & 1)) 1) colSwap = n - colSwap;
} autre { // même taille de la planche
rowSwap = Math.min(rowSwap, n - rowSwap);
colSwap = Math.min(colSwap, n - colSwap);
}

- Oui. 5. Réponse finale
retour (rowSwap + colSwap) / 2;
}
}
«» "

---

- Oui. 9. Mise en œuvre de Python

'`python
"""
LeetCode 782 - Transformer en Chessboard
Solution Python 3 – temps O(n^2), espace O(1)
"""

Solution de classe:
def movesToChessboard(self, board: list[list[int]]) -> Int:
n = len(board)
ligne_sum = col_sum = 0
ligne_swap = col_swap = 0

1. Vérification de faisabilité
pour r dans la plage(n):
pour c dans la plage(n):
si [board[0][0] ^board[r][0] ^board[0][c] ^board[r][c] & 1:
retour -1

2. Compter les lignes/cols qui correspondent
pour i dans la plage(n):
row_sum += planche[0][i]
col_sum += planche[i][0]
if board[i][0]== (i & 1): row_swap += 1
Si la planche[0][i]] == (i & 1): col_swap += 1

3. Valider un compte
sinon (n//2 <= range_sum <= (n+1)//2): retour -1
si non (n//2 <= col_sum <= (n+1)//2): retour -1

4. Ajuster les swaps sur la base de la parité
si n % 2:
si ligne_swap % 2: ligne_swap = n - ligne_swap
si col_swap % 2: col_swap = n - col_swap
Sinon:
row_swap = min(row_swap, n - row_swap)
(col_swap, n - col_swap)

5. Retourner des mouvements minimes
retour (row_swap + col_swap) // 2
«» "

---

10. Mise en œuvre C++

'`cpp
***
* 782. Transformer en tableau d'échecs
*
* Solution C++: temps O(n^2), espace O(1).
* Utilise la même stratégie de comptage optimale.
*/
solution de classe {
public:
int movesToChessboard(vector<vector<int>>&board) {
int n = board.size();
dans la rangéeSum = 0, colSum = 0; // nombre de 1s dans la première rangée/colonne
int rowSwap = 0, colSwap = 0; // rows/cols déjà en bonne parité

- Oui. 1. Contrôle de faisabilité
pour (int r = 0; r < n; ++r) {
pour (int c = 0; c < n; ++c) {
si [(planche[0]]0] ^ planche[r]0] ^ planche[0]c] ^ planche[r][c]) et 1) {
retour -1;
}
}
}

- Oui. 2. Compter les rangées/cols qui correspondent à --------- */
pour (int i = 0; i < n; ++i) {
la ligneSum += planche[0][i];
le colSum += planche[i][0];
Si (board[i][0] == (i & 1)) ++rowSwap;
Si (board[0][i] == (i & 1)) ++colSwap;
}

- Oui. 3. Valider 1 compte --------- */
si (rowSum < n/2.
si (colSum < n/2.

- Oui. 4. Ajustement des swaps sur la base de la parité --------- */
si (n & 1) { // impair
si (rowSwap & 1) rowSwap = n - rowSwap;
si (colSwap et 1) colSwap = n - colSwap;
} autre { // même
rowSwap = min(rowSwap, n - rowSwap);
colSwap = min(colSwap, n - colSwap);
}

- Oui. 5. Réponse finale
retour (rowSwap + colSwap) / 2;
}
};
«» "

---

- Oui. 11. Mise en œuvre

«» c
***
* 782. Transformer en tableau d'échecs
*
* Solution C – temps O(n^2), espace O(1).
* Ecrit en C pour une portabilité maximale.
*/
int movesToChessboard(int** board, int n) {
dans la rangéeSum = 0, colSum = 0;
dans la rangéeSwap = 0, colSwap = 0;

- Oui. 1. Contrôle de faisabilité
pour (int r = 0; r < n; r++) {
pour (int c = 0; c < n; c++) {
si [(planche[0][0] ^ planche[r][0] ^ planche[0][c] ^ planche[r][c] et 1)
retour -1;
}
}

- Oui. 2. Compter les rangées/cols qui correspondent à --------- */
pour (int i = 0; i < n; i++) {
la ligneSum += planche[0][i];
le colSum += planche[i][0];
si (board[i][0]== (i & 1)) ligneSwap++;
si (board[0] [i] == (i & 1)) colSwap++;
}

- Oui. 3. Valider 1 compte --------- */
si (rowSum < n/2.
si (colSum < n/2.

- Oui. 4. Ajustement des swaps sur la base de la parité --------- */
si (n & 1) { // impair
si (rowSwap & 1) rowSwap = n - rowSwap;
si (colSwap et 1) colSwap = n - colSwap;
} autre { // même
rowSwap = rowSwap < n-rowSwap ? range : n-rowSwap;
colSwap = colSwap < n-colSwap ? Le présent règlement entre en vigueur le jour suivant celui de sa publication au Journal officiel de l'Union européenne.
}

- Oui. 5. Réponse finale
retour (rowSwap + colSwap) / 2;
}
«» "

> **Note:** En C, `int** board` est supposé être un tableau carré 2-D.

---

12. Récapitulation et retrait

* **Optimalité** – l'algorithme permet les swaps *fewest* possibles.
* **Simplicité** – quelques compteurs entiers ; aucune structure de données lourde.
* **Robustness** – s'occupe de tailles impaires / paires, contrôles de fréquence, ajustements de parité.
* **Performance** – `O(n2)` est trivial pour `n ≤ 30`, mais des échelles agréablement pour des entrées plus grandes.

Cette solution est un favori dans mon répertoire d'interviews et s'est avérée à la fois *fast* et *clean*.

---

Réflexions finales

Transformer un tableau en tableau de bord n'est pas seulement à propos d'échanger ; il est à propos de comprendre les contraintes algébriques sous-jacentes et de tirer parti de la parité. En traitant les lignes et les colonnes symétriquement et en comptant astucieusement les erreurs, nous pouvons calculer le nombre minimal de mouvements avec un seul passage sur la matrice.

Bon codage, et bonne chance pour écraser cette interview de LeetCode! C'est ce qu'il a dit.

---


> * Si vous avez aimé cette plongée profonde, consultez mes autres explications d'algorithme : [160. Intersection de deux tableaux II](https://leetcode.com/problems/intersection-of-two-arrays-ii/), [1729. Swapping Nodes in a Linked List](https://leetcode.com/problems/swapping-nodes-in-a-linked-list/).*