---
titre: LeetCode 3242. Design Neighbor Sum Service - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Aperçu du problème

**Design Neighbor Sum Service** – un problème de style LeetCode qui vous demande de soutenir deux requêtes à temps constant sur une grille *n × n* :

Qu'est-ce qu'il faut calculer ?
- C'est pas vrai.
"adjacentSum(valeur)" Somme des quatre voisins cardinaux (en haut, en bas, à gauche, à droite) qui existent. Autres
"diagonalSum(valeur)""Somme des quatre voisins diagonaux (en haut à gauche, en haut à droite, en bas à gauche, en bas à droite) qui existent. Autres

La grille contient **entiers distincts**, `0 ≤ valeur < n2` et `n` satisfait `3 ≤ n ≤ 50`.
Vous recevrez jusqu'à «2·105» requêtes – le service doit répondre à chaque requête en **O(1)** temps.

> **Pourquoi ce problème est important pour votre préparation d'entrevue* *
> De nombreuses questions liées à la structure des données dans les entrevues technologiques tournent autour de *grid* traversal et *hash-mapping*. La maîtrise de ce problème vous donne un motif réutilisable pour les problèmes de valeur, un must-know pour toute interview Java, Python ou C++.

---

- Oui. 2. Conception – - Bon, mauvais et ugly

Aspect du bien
- C'est quoi ?
**Pre-processing** Cela convertit une recherche naïve O(n2) par requête en O(1). Autres Ne rien faire – chaque requête numériserait toute la grille. Construire un gigantesque tableau 3-D (ligne, col, valeur) qui est gaspillé. Autres
**Mémorie**=Enregistrez la grille comme-est (`vector<vector<int>>` / `int[][]`) plus une carte (`unordered_map<int, pair<int,int>>). Attribuer des coordonnées temporaires à chaque requête. Récursivement rechercher la grille sur chaque appel – empiler le risque de débordement sur les grandes grilles. Autres
**Manipulation d'un cas d'Edge**= Vérifications explicites des limites (`i>0`, `i<n-1`, ...).= Oubliez de gérer les bordures → `IndexOutOfBounds`.== Utiliser l'indexation basée sur 1 mais la grille est basée sur 0 → erreurs hors-par-un. Autres
**Readability**= Effacer les noms de méthode, les commentaires et une simple classe de données pour les paires de coordonnées.= Trop de variables globales, état caché. Une récursion ou des hacks lambda trop compliqués qui nuisent à la durabilité. Autres

** Ligne de bottom** – La conception de « good » utilise un **hash‐map** pour la recherche instantanée, maintient le code propre et gère les bordures en toute sécurité. La variante "bad" est la recherche de force brute; la variante "ugly" mélange la logique récursive avec l'état mutable partagé, ce qui rend difficile à raisonner.

---

- Oui. 3. Exécution

#### 3.1 Java (O(1) demande avec `HashMap`)

"Java
Importer java.util. HashMap;
Importer java.util. Carte;

***
* Conception de service de somme de voisinage
* https://leetcode.com/problèmes/design-neighbor-sum-service
*
* Complexité temporelle
* Construction : O(n2)
* Demandes de renseignements : O(1)
*
* Complexité spatiale
* O(n2) pour la grille + O(n2) pour la carte de hachage
*
* Auteur : [Votre nom]
* Date: 2024‐08‐31
*/
Quartier général Somme {

/** matrice originale */
matrice privée finale int[];
Taille de la grille
final privé n;
/** valeur -> (ligne, col) */
carte finale privée<entier, int[]> indexMap;

/** Constructeur: grille préprocédée en O(n2) */
public NeighborSum(int[][] grille) {
c.n = longueur de la grille;
Ça. matrice = nouvelle int[n][n];
ce.indexMap = nouvelle HashMap<>(n * n);

pour (int i = 0; i < n; i++) {
pour (int j = 0; j < n; j++) {
int val = grille[i][j];
matrice[i][j] = valeur;
indexMap.put(val, nouvelle int[]{i, j});
}
}
}

*** Somme des voisins adjacents (haut, bas, gauche, droite) */
Int public adjacentSum(valeur int) {
int[] pos = indexMap.get(valeur);
i = pos[0], j = pos[1];
= 0;

si (i > 0) somme += matrice[i - 1] [j]; // haut
si (i + 1 < n) somme += matrice[i + 1] [j]; // bas
si (j > 0) somme += matrice[i][j - 1]; // gauche
si (j + 1 < n) somme += matrice[i][j + 1]; // droite
la somme de retour;
}

*** Somme des voisins diagonaux (4 diagonales) */
diagonale publique int Somme (valeur intégrale) {
int[] pos = indexMap.get(valeur);
i = pos[0], j = pos[1];
= 0;

Si (i > 0 & & j > 0) somme += matrice[i - 1][j - 1]; // en haut à gauche
si (i > 0 && j + 1 < n) somme += matrice[i - 1][j + 1]; // en haut à droite
si (i + 1 < n && j > 0) somme += matrice[i + 1][j - 1]; // en bas à gauche
si (i + 1 < n && j + 1 < n) somme += matrice[i + 1][j + 1]; // bas à droite
la somme de retour;
}

/** ---------------- Démo */
public statique vide principal(String[] args) {
int[[]] grille = {
{0, 1, 2},
{3, 4, 5},
{6, 7, 8}
};
NeighborSum ns = nouveau NeighborSum(grid);

Système.out.println("adjacentSum(4) = " + ns.adjacentSum(4)); // 16
Système.out.println("diagonalSum(4) = " + ns.diagonalSum(4)); // 16
}
}
«» "

---

3.2 Python 3

'`python
# Design Neighbor Sum Service – Implémentation de Python
♪ Complexité temporelle: Construction O(n2), requêtes O(1)
♪ Complexité spatiale: O(n2)

classe VoisinSum:
def __init_(self, grille):
"""
:param grid: List[List[int]] – n x n matrice d'entiers distincts
"""
auto.n = len(grid)
auto.grid = grille
# Valeur de la carte -> (ligne, col)
Self.idx = {grid[i][j]: (i, j) pour i dans la plage (self.n) pour j dans la plage (self.n)}

à proximité Somme (même, valeur: int) -> Int:
i, j = auto.idx[valeur]
s = 0
Si i > 0: s += auto.grid[i - 1][j] # haut
si i + 1 < self.n: s += self.grid[i + 1]
si j > 0: s += self.grid[i][j - 1] # gauche
si j + 1 < self.n: s += self.grid[i][j + 1] # droite
retour s

def diagonale Somme (même, valeur: int) -> Int:
i, j = auto.idx[valeur]
s = 0
i i > 0 et j > 0: s += self.grid[i - 1][j - 1] # haut à gauche
i > 0 et j + 1 < self.n: s += self.grid[i - 1][j + 1] # haut à droite
si i + 1 < self.n et j > 0: s += self.grid[i + 1][j - 1] # bas– gauche
si i + 1 < self.n et j + 1 < self.n: s += self.grid[i + 1][j + 1] # bas à droite
retour s

♪ Démo
si __nom__ == "__main__" :
quadrillage = [[0, 1, 2], [3, 4, 5], [6, 7, 8]]
ns = voisinSum(grid)
print(ns.adjacentSum(4)) # 16
print(ns.diagonalSum(4)) # 16
«» "

---

### 3.3 C++17 (Vecteur + Carte_non ordonnée)

'`cpp
// Design Neighbor Sum Service – implémentation C++17
// Compiler avec: g++ -std=c++17 -O2 -Wall neighbour_sum.cpp -o neighbour_sum

#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

classe VoisinSum {
public:
NeighborSum(vecteur Const<vecteur<int>>& grille)
: n(grid.size()), matrice(grid)
{
// Construire une carte de hachage : valeur -> (ligne, col)
pour (int i = 0; i < n; ++i)
pour (int j = 0; j < n; ++j)
Pos[grid[i][j]] = {i, j};
}

int adjacentSum(int) const {
auto [i, j] = pos.at(valeur);
= 0;
si (i > 0) somme += matrice[i - 1] [j]; // haut
si (i + 1 < n) somme += matrice[i + 1] [j]; // bas
si (j > 0) somme += matrice[i][j - 1]; // gauche
si (j + 1 < n) somme += matrice[i][j + 1]; // droite
la somme de retour;
}

diagonale int Sum(int valeur) const {
auto [i, j] = pos.at(valeur);
= 0;
Si (i > 0 & & j > 0) somme += matrice[i - 1][j - 1]; // en haut à gauche
si (i > 0 && j + 1 < n) somme += matrice[i - 1][j + 1]; // en haut à droite
si (i + 1 < n && j > 0) somme += matrice[i + 1][j - 1]; // en bas à gauche
si (i + 1 < n && j + 1 < n) somme += matrice[i + 1][j + 1]; // bas à droite
la somme de retour;
}

particulier:
l'élément n;
matrice vectorielle<vector<int>>;
non ordonné_map<int, paire<int,int>> pos; // valeur -> coordonnées
};

/* - Oui. Démo -------- */
Int main() {
vector<vector<int>> grille = {
{0, 1, 2},
{3, 4, 5},
{6, 7, 8}
};

NeighborSum ns(grid);
<< "adjacentSum(4) = " < ns.adjacentSum(4) << '\n'; // 16
<< "diagonalSum(4) = " < ns.diagonalSum(4) << '\n'; // 16
}
«» "

---

- Oui. 4. Pièges communs et comment les éviter

Piège
- Oui.
**O(n2) scanner par requête**=Enregistrer les coordonnées dans une carte de hachage (`valeur → (ligne, col)`). Autres
**Vérifications des limites manquantes**= Toujours garder avec `si (row>0)`, `si (col<n-1)` ... avant d'accéder à `matrix[row][col]`. Autres
** Erreurs hors-par-un**= Stick to 0-based indexing for the both and the map. Autres
**Mutable état partagé dans la récursion** Autres

---

- Oui. 5. Conseils d'entrevue

1. ** Expliquez la carte d'abord** – Il faut pré-calculer une table de recherche pour que chaque requête soit O(1). (en milliers de dollars)
2. **Afficher la logique de la frontière** – Remarquez que la rangée supérieure n'a pas de "haute" voisin, donc nous gardons avec `row>0`. (en milliers de dollars)
3. **Parler des compromis avec la mémoire** – La grille elle-même est O(n2), la carte est également O(n2). Vu `n ≤ 50`, c'est trivial pour les serveurs modernes. (en milliers de dollars)
4. **Utilisez une fonction propre et testable** – écrivez un petit `demo()` ou `main()` qui imprime les valeurs attendues; les intervieweurs adorent voir des vérifications rapides de correction.
5. **Mathématiques de complexité temporelle** – La construction fait 2 500 pas pour une grille 50×50; chaque requête n'est que 4 ou 8 recherches, c'est-à-dire un temps constant. (en milliers de dollars)

---

- Oui. 6. Décollage final

Le problème *Design Neighbor Sum Service* est un modèle** pour les intervieweurs et les personnes interrogées :

* **Prétraitement + plan de hachage** = recherche instantanée, bordures sûres, code propre.
* Recherche Brute-force = trop lente et sujette à erreur.
* Les solutions récursives de type "gugly" nuisent à la lisibilité et peuvent se briser sur de grandes entrées.

En maîtrisant la solution « good » dans **Java, Python et C++**, vous aurez une boîte à outils réutilisable pour les questions de recherche de valeur par valeur** qui apparaissent dans presque chaque interview technique. Bonne chance – votre prochaine ronde de codage est maintenant un peu plus facile à casser!