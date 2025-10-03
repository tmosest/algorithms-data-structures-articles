---
titre: LeetCode 723. Crush aux bonbons -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code de solution
Ci-dessous sont **trois implémentations complètes, autonomes** du résolveur Candy Crush
(LeetCode 723) dans **Java**, **Python 3** et **C++**.
Chaque solution suit la même idée algorithmique :

1. ** Marquez** toutes les bonbons qui appartiennent à un parcours horizontal ou vertical ≥ 3.
2. **Crush** les bonbons marqués → les définir à `0`.
3. **Drop** bonbons dans chaque colonne jusqu'à ce que la planche se stabilise.
4. Répétez jusqu'à ce que plus de bonbons ne puissent être écrasés.

Les trois codes sont prêts à copier-coller dans l'éditeur de LeetCode ou tout IDE.

---

### A. Java (Code de bord 723)

"Java
Importation de java.util.*;

solution de classe {
Int m, n;

public int[][] bondageCrush(int[][] plan) {
m = longueur de la planche;
n = longueur de la planche[0];
pendant que (!crush(board)) {
Drop(board);
}
la pension de retour;
}

/* Revenez vrai si la planche est stable, faux si on a écrasé quelque chose. */
écrasement booléen privé(int[][]) {
stable booléenne = vrai;
// 1. Marquer les cellules qui doivent être écrasées
pour (int r = 0; r < m; r++) {
pour (int c = 0; c < n; c++) {
si [bord[r][c]] 0) poursuivre;
val int = Math.abs(board[r][c]);

booléen horizontal = faux, vertical = faux;
si (c > 0 && c < n - 1 &&
Math.abs(board[r][c - 1]) == Val &&
Math.abs(board[r][c + 1]) == val) {
horizontal = vrai;
}
si (r > 0 && r < m - 1 &&
Math.abs(board[r - 1][c]) == Val &&
Math.abs(board[r + 1][c]) == val) {
verticale = vrai;
}

Si (horizontale) {
stable = faux;
Tableau[r][c] = -Math.abs(tableau[r][c]); // marques négatives écraser
si (horizontale) {
board[r][c - 1] = -Math.abs[r][c - 1];
la planche[r][c + 1] = -Math.abs(la planche[r][c + 1]);
}
si (vertical) {
la planche[r - 1][c] = -Math.abs(la planche[r - 1][c]);
la planche[r + 1][c] = -Math.abs(la planche[r + 1][c]);
}
}
}
}

// 2. Supprimer les cellules marquées
pour (int r = 0; r < m; r++) {
pour (int c = 0; c < n; c++) {
si (board[r][c] < 0)board[r][c] = 0;
}
}
retour stable;
}

/* Faire tomber les bonbons pour remplir les cellules zéro */
vide privé drop(int[][]) {
pour (int c = 0; c < n; c++) {
int write = m - 1; // position suivante pour écrire non-zéro
pour (int r = m - 1; r >= 0; r--) {
si [bord[r][c] != 0) {
tableau[écrire][c] = tableau[r][c];
si (écrire != r) planche[r][c] = 0;
écrire...
}
}
}
}
}
«» "

---

B. Python 3

'`python
Solution de classe:
def bondageCrush(self, board: List[List[int]]) -> Liste[Liste[int]]:
m, n = len(board), len(board[0])

def écraser() -> C'est vrai.
""Retour Vrai si la planche est stable."""
= Faux
Marque
pour r dans la plage(m):
pour c dans la plage(n):
si la planche[r][c]] 0:
poursuivre
val = abs(board[r][c])
hor = Faux
ver = Faux
si 0 < c < n - 1 et \
abs(board[r][c - 1]) == val et \
Abs(board[r][c + 1]) == Valeur
hor = Vrai
si 0 < r < m - 1 et \
abs(board[r - 1][c]) == val et \
abs(board[r + 1][c]) == Val:
ver = Vrai
si hor ou ver:
= Vrai
board[r][c] = -abs[r][c]
Si hor:
board[r][c - 1] = -abs[r][c - 1]
board[r][c + 1] = -abs[r][c + 1]
si:
board[r - 1][c] = -abs[r - 1][c]
tableau[r + 1][c] = -abs[r + 1][c]

Écraser
pour r dans la plage(m):
pour c dans la plage(n):
si la planche[r][c] < 0:
tableau[r][c] = 0
retour non modifié

def drop() -> Aucun:
""" colonne "Candies de trop par colonne."""
pour c dans la plage(n):
écrire = m - 1
pour r dans la plage (m - 1, -1, -1):
si planche[r][c] != 0:
board[write][c] = board[r][c]
si écrire != r:
tableau[r][c] = 0
écrire -= 1

sans écraser():
goutte()
tableau de retour
«» "

---

### C. C++ (Code Leet 723)

'`cpp
solution de classe {
public:
vector<vector<int>> bondageCrush(vector<vector<int>>&board) {
int m = board.size(), n = board[0].size();
pendant que (!crush(board)) drop(board);
la pension de retour;
}

particulier:
Bool Crush(vecteur<vecteur<int>> et planche) {
int m = board.size(), n = board[0].size();
bool stable = true;

// 1. Marquer les cellules à écraser
pour (int r = 0; r < m; ++r) {
pour (int c = 0; c < n; ++c) {
si [bord[r][c]] 0) poursuivre;
val int = abs(board[r][c]);

bool hor = false, ver = false;
si (c > 0 && c < n-1 &&
abs(board[r][c-1]) ==val && abs(board[r][c+1])==val = true;
si (r > 0 && r < m-1 &&
abs(board[r-1][c])==val && abs(board[r+1][c]==val] ver = true;

si (hors de) {
stable = faux;
la planche[r][c] = -abs[r][c];
si (hors) {
board[r][c-1] = -abs[r][c-1];
board[r][c+1] = -abs[r][c+1];
}
si (ver) {
la planche[r-1][c] = -abs[r-1][c];
la planche[r+1][c] = -abs[r+1][c];
}
}
}
}

// 2. Crush (réglage à 0)
pour (auto &row : carte)
pour (int &x : ligne)
si (x < 0) x = 0;

retour stable;
}

vide drop(vector<vector<int>&board) {
int m = board.size(), n = board[0].size();
pour (int c = 0; c < n; ++c) {
int write = m-1; // ligne libre suivante du bas
pour (int r = m-1; r >= 0; --r) {
si [bord[r][c] != 0) {
tableau[écrire][c] = tableau[r][c];
si (écrire != r) planche[r][c] = 0;
--écrire;
}
}
}
}
};
«» "

---

Article du blog – Code de Leet 723 (Crush Candy): Un Java-Python-C++ Guide pour les entrevues d'emploi

> **Titre**:
> **Code de leet d'écrasement 723** – *Un Java/Python/C++ complet Guide de réussite des entrevues*

> ** Mots clés du référencement**:
> `Candy Crush LeetCode`, `LeetCode 723 solution`, `Candy Crush algorithme`, `Java Python C++ solutions`, `algorithme d'entretien d'emploi`, `conseils d'entretien technologique "

---

Table des matières

1. [Introduction] (#introduction)
2. [Résumé des problèmes] (#résumé des problèmes)
3. [Défis clés] (#les défis clés)
4. [Aperçu de la solution] (#solution-overview)
5. [Détails de mise en œuvre] (#détails de mise en œuvre)
6. [Code Snippets](#code-snippets)
7. [Analyse de la complexité] (#analyse de la complexité)
8. [Bonne, mauvaise et mauvaise] (#Bonne et mauvaise)
9. [Conseils d'entrevue](#interview-tips)
10. [Conclusion] (#conclusion)

---

Introduction

Candy Crush (LeetCode 723) est un puzzle classique de grille 2D qui mélange *recherche* et *physique*.
Il est souvent demandé dans les entrevues de structure de données parce qu'il oblige les candidats à penser à:

- **Opérations simultanées** (écrasement de toutes les pistes en même temps)
- ** mutation d'état** (marque négative)
- ** Mécanique gravitationnelle**

La maîtrise de ce problème démontre la maîtrise des tableaux, des boucles et des changements d'état itératifs – tous **doivent** pour une entrevue d'ingénierie logicielle.

---

Résumé du problème

Avec une matrice `board[m][n]` (chaque cellule contient un entier > 0 ou `0` pour vide),
**Répéter** jusqu'à ce que plus de bonbons ne puissent être écrasés:

1. Tout parcours de 3 ou plus **candies adjacentes** horizontalement ou verticalement doit être écrasé.
2. Les bonbons écrasés se transforment en `0` (vide).
3. Tout bonbon qui a un `0` au-dessous tombe ** vers le bas** jusqu'à ce qu'il frappe un autre bonbon ou le fond.

Retourne la dernière planche stable.

Contraintes:

- `1 ≤ m, n ≤ 30`
- `1 ≤ planche[i][j] ≤ 1000` (sauf 0 pour vide)

---

C'est vrai. Principaux défis

Pourquoi ça compte ?
-- -- -- -- -- -- -- -- --
**L'écrasement simultané**Toutes les courses doivent disparaître **une fois**; l'écrasement partiel donne une mauvaise réponse. Crushing pendant la numérisation – conduit à des erreurs de cascade. Autres
**Marquage vs concassage**= Des marques négatives sont nécessaires pour qu'un bonbon dans une course ne soit pas écrasé deux fois. Oublier de démarquer → boucle infinie. Autres
Après chaque écrasement, les bonbons peuvent créer de nouveaux runs. Utiliser l'approche de type pile incorrectement → O(m2n) au lieu de O(mn). Autres
**Cellules d'Edge** Erreurs hors‐par‐un (par exemple, vérification de «c+1» dans la dernière colonne). Autres

---

Aperçu de la solution

1. **Marque**
* Scanner toute la planche.
* Pour chaque cellule non zéro, cochez la case gauche/droite et les voisins haut/bas.
* Si un parcours ≥ 3 existe horizontalement ou verticalement, marquez toutes les cellules concernées en les rendant négatives.
* Gardez un drapeau « changé » – si une cellule est marquée, nous avons besoin d'une autre itération.

2. **Crush**
* Toutes les cellules négatives deviennent `0`.
* Si aucune cellule n'a été marquée, la carte est *stable* → boucle de sortie.

3. **Dépôt**
* Pour chaque colonne, déplacer toutes les cellules non zéro vers le bas (technique de pointeur d'écriture).
* Réglez les cellules supérieures restantes à `0`.

4. **Répéter** jusqu'à ce que la planche se stabilise.

L'algorithme est **in-place** (O(1) espace supplémentaire) et fonctionne jusqu'à ce qu'il n'y ait plus d'écrasement.

---

Détails de la mise en œuvre

La langue mise en évidence Notes
C'est pas vrai.
**Java**= Utilise `Math.abs` pour ignorer les marques, le marquage négatif, le pointeur d'écriture. Évite de copier toute la planche; O(m n) peritération. Autres
**Python**= Utiliser `abs` pour éviter les changements de signe, lister les compréhensions pour la clarté. Leverages Python est le typage dynamique; toujours O(m n) peritération. Autres
**C++**="vector<vector<int>>=" + `abs`, marquage négatif, simple pour les boucles. Utiliser l'index `write` pour une chute efficace. Autres

Toutes les implémentations sont compatibles avec le juge en ligne LeetCode.

---

Analyse de complexité

Laissez `m` = lignes, `n` = colonnes.

* **Pourcentage**
* Marque + écrasement : **O(m n)**
* Drop: **O(m n)** (chaque colonne scanne une fois)

* **Nombre d'itérations**
Dans le pire des cas, chaque itération enlève au moins un bonbon.
Étant donné qu ' il existe au plus des bonbons `m n`, le nombre d ' itérations ≤ `m n`.

* **Temps total**
"O(m n * itérations)" → **O(m n)2)** dans le pire des cas absolus,
mais généralement **O(m n)** pour les tableaux aléatoires.

* **Espace**
En place: **O(1)** auxiliaire.
(Le `board' de LeetCode lui-même est compté comme entrée.)

---

### # # # # #% Bonne, mauvaise et moche

Aspect du bien
- C'est quoi ?
**Bon** • Itératif, facile à comprendre. <br>• Poigne les écrasements simultanés correctement. <br>• Fonctionne pour tous les cas de bord (cours aux frontières).
**Le mauvais**Le marquage négatif peut ne pas être intuitif pour les intervieweurs. <br>• La verbosité du code peut masquer les bugs si elle n'est pas soigneusement cochée.
**Ugly**Ugly**Ugly • Utilisation de tableaux 3-D temporaires pour tenir des marques. <br>• Appel récursivement concasseur/goutte conduisant au débordement de la pile sur de grandes planches. <br>• Ne pas réinitialiser `changed` flag → boucle infinie. Autres

> **Conseil pro**: Commencez toujours par écrire une fonction d'aide qui *détecte* une course, puis *application* écraser et *application* tomber. Il maintient la logique propre et réduit les erreurs off-by-one.

---

Conseils d'entrevue

1. ** Expliquez la stratégie de marquage négatif** – pourquoi elle est nécessaire et comment elle évite le cascade.
2. **Parcourez un petit exemple** sur le papier (par exemple, tableau 4×4).
3. **Modalités alternatives** (p. ex. BFS/DFS pour les parcours) et pourquoi elles sont moins efficaces.
4. **Afficher les tests d'unité**: les parcours de couverture qui se chevauchent, les parcours aux coins et l'écrasement complet de la planche.
5. **Discuse la complexité du temps** – montrez que vous comprenez la nature itérative.
6. **Demandez des questions** – si vous n'êtes pas sûr de la partie "gravité", posez des questions claires.

> *Rappelez-vous*: Les intervieweurs sont plus intéressés par votre *processus de réflexion* que le code final.

---

Conclusion

Candy Crush (LeetCode 723) est plus qu'un puzzle – c'est une référence pour:

- **La pensée algorithmique* *
- **Manipulation de l'état en place**
- **Connaissance au cas par cas**

L'astuce de marquage *négatif, associée à la chute du pointeur d'écriture, donne un code propre, efficace et prêt à l'entrevue.

En maîtrisant ce problème à travers **Java, Python et C++**, vous serez bien préparé pour toute question *grid-simulation* qui apparaît dans votre prochain entretien technique.

---

> **À emporter**:
> *Lorsque vous pouvez implémenter une carte Candy Crush stable dans moins de 100 lignes de code, vous avez montré que vous pouvez gérer des simulations d'état — une compétence clé pour tout moteur ou ingénieur système. *

---

> *Vous voulez plus d'entrevue ? Consultez notre série sur **Fenêtre coulissante sur les grilles 2D**, **Graph Traversals** et **Programmation dynamique**. *

---

> *Auteur*: **[Votre nom]** – *Ingénieur logiciel principal et coach d'entrevue*
> * Publié* : **mars 2024**
> *Mise à jour*: **Avril 2024** – Ajout de la mise en œuvre C++.

---

**Codage heureux & bonne chance avec vos interviews!**

---

N'hésitez pas à adapter ou à agrandir l'article pour votre blog personnel ou votre contenu tech‐career.