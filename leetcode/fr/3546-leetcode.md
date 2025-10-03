---
Titre: LeetCode 3546. Partition de la grille de somme égale Je...
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Egal-Sum Grille Partition I – Les bons, les mauvais et les méchants
> **SEO Mots-clés:** Equal Sum Grid Partition, Leetcode 3546, entretien d'emploi, solution Java, solution Python, solution C++, programmation dynamique, préfixe, entretien d'algorithme

---

- Oui. 1. Pourquoi ce problème vous fait penser

- **Codage à gauche 3546** – un problème de niveau *Moyenne* que de nombreux rôles de front-end, back-end et d'ingénierie des données posent lors d'une entrevue de codage.
- Oui. La question teste quelques concepts de base :
- Traversée du réseau 2-D
- Préfixe / montants cumulés
- Manipulation des caisses
- complexité optimale du temps et de l'espace
- Oui. C'est court, mais c'est un problème *classique* qui vous montre comment convertir une idée de force brute en solution **O(m + n)**.

Si vous pouvez clouer ceci, vous aurez l'air d'un candidat solide qui sait résoudre efficacement les problèmes de matrice.

---

- Oui. 2. Rétablissement du problème

Compte tenu d ' une grille < < m × n > > de nombre entiers ** positifs** :

«» "
grille[i][j] (0 ≤ i < m, 0 ≤ j < n)
«» "

Vous pouvez faire **exactement une** coupe – horizontale (entre deux lignes) ou verticale (entre deux colonnes) – qui divise la grille en deux parties non vides.
Return `true` si les deux parties peuvent avoir **des sommes égales**, sinon `faux`.

Contraintes
- `1 ≤ m, n ≤ 10^5`
- "2 ≤ m * n ≤ 10^5"
- `1 ≤ grille[i][j] ≤ 10^5`

---

- Oui. 3. Intuition – DON=T Scanner la grille entière à chaque fois

Une approche naïve serait :

1. Essayez chaque coupe horizontale, calculez la somme de la moitié supérieure chaque fois → **O(m × n)**
2. Essayez chaque coupe verticale de la même façon → **O(m × n)**

Avec `m * n` jusqu`à `10^5`, c`est bien, mais nous pouvons faire mieux.

**Observation principale** – La somme des premières lignes *k* dépend uniquement de la somme de chaque ligne, et non des cellules individuelles à l'intérieur de ces lignes.
Même pour les colonnes.

Donc nous pouvons:

1. Calculer les sommes de la ligne** («rowSum[i] = -[i][j]» – «O(m × n)»
2. Calculer les sommes de la colonne** (colSum[j] = grille de calcul [i][j]» – «O(m × n)»
3. Calculer les montants de préfixe sur `rowSum` et `colSum` – `O(m + n) "
4. Comparer les valeurs préfixes à la somme totale – **O(m + n)**

Total: **O(m × n)** temps, **O(m + n)** espace supplémentaire – optimal.

---

- Oui. 4.

1. **Lisez la grille** et déterminez `m` (lignes) et `n` (colonnes).
2. **Initialiser** deux longs tableaux
- `rowSum[m]` – somme cumulative de chaque ligne
- «colSum[n]» – somme cumulative de chaque colonne
3. **Première passe** (une seule boucle sur toutes les cellules):
"Java
pour i en 0.m-1:
pour j en 0..n-1:
val = grille[i][j];
rowSum[i] += valeur;
C'est la première fois que l'on s'en occupe. valeur;
«» "
L'utilisation de `long` nous protège contre le débordement (`maximum total de 10^10').
4. Calcul de la somme totale**: < < Total = < rangSum > > (même que < < colSum > > ).
5. **Vérification de la coupe horizontale**:
"Java
longueur supérieure = 0;
pour i en 0.m-2: // la coupe doit laisser au moins une rangée en dessous
supérieur += rangSum[i];
si (upper) = total - supérieur) retour vrai;
«» "
6. **Vérification de la coupe verticale**:
"Java
longue gauche = 0;
pour j en 0..n-2:
gauche += colSum[j];
si (gauche == total - gauche) retourner vrai;
«» "
7. **Retour** "faux" si aucune coupe ne fonctionne.

---

- Oui. 5. Les cas de bord et l'Ugly

Autres Décision Pourquoi ça compte ?
- - - - - - - - - - Non.
1` (une seule ligne) , seulement des coupes verticales possibles , Loop `m-2` devient `-1` → aucune itération
- Oui. 1'-- Seulement des coupes horizontales possibles.
= = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = =
Grille de taille `1×2` ou `2×1`.Une seule coupe, vérifier correctement.Les boucles gèrent correctement la seule coupe possible.
Autres Somme totale impair. Impossible de diviser également. Les boucles ne satisferont jamais l'égalité; nous pourrions sortir tôt si "total % 2 != 0', mais pas nécessaire. Autres

---

- Oui. 6. Code

Voici des implémentations idiomatiques propres dans **Java**, **Python** et **C++**.
Chaque version suit la même logique et tourne dans **O(m × n)** temps et **O(m + n)** espace.

#### 6.1 Java

"Java
***
* Leetcode 3546 – Partage de la grille de somme égale Les
* Mise en œuvre de Java 17 en utilisant des montants préfixés.
*/
solution de classe publique {
pulvérisateur public de booléenPartitionGrid(int[][]) {
int m = longueur de la grille; // lignes
int n = grille[0].longueur; // colonnes

longue[] ligneSum = nouvelle longue[m];
long[] colSum = nouveau long[n];
long total = 0L;

// Premier passage: build range and column sums
pour (int i = 0; i < m; i++) {
pour (int j = 0; j < n; j++) {
val longue = grille[i][j];
rowSum[i] += valeur;
C'est la première fois que l'on s'en occupe. valeur;
total += valeur; // total peut être calculé ici
}
}

// Coupes horizontales
longueur supérieure = 0L;
pour (int i = 0; i < m - 1; i++) {
supérieur += rangSum[i];
si (supérieure à ) total - supérieur) {
retour vrai;
}
}

// Coupes verticales
longue gauche = 0L;
pour (int j = 0; j < n - 1; j++) {
gauche += colSum[j];
if (gauche == total - gauche) {
retour vrai;
}
}

retourner faux;
}
}
«» "

> **Pourquoi "long"?**
> Le produit `m * n` peut être 105 et chaque cellule jusqu'à 105 → somme max 1010 < 263, mais dépasse toujours 32 bits.

6.2 Python

'`python
"""
Leetcode 3546 – Partage de la grille de somme égale Les
Implémentation Python 3 en utilisant des sommes préfixes.
"""

def can_partition_grid(grid):
m, n = len(grid), len(grid[0])
row_sum = [0] * m
col_sum = [0] * n
Total = 0

# Construire des montants de ligne et de colonne
pour i dans la plage (m):
pour j dans la plage(n):
val = grille[i][j]
ligne_sum[i] += valeur
_somme[j] += valeur
Total += valeur

# Coupes horizontales
supérieur = 0
pour i dans la plage (m - 1):
supérieur += ligne_sum[i]
Si supérieur == total - supérieur:
retour Vrai

# Coupes verticales
gauche = 0
pour j dans la plage (n - 1):
gauche += col_sum[j]
si gauche == total - gauche:
retour Vrai

Retour Faux
«» "

> **Pourquoi ne pas utiliser `numpy`? **
> Les contraintes de problème sont assez petites pour les boucles Python pures, ce qui maintient la solution plate-forme-agnostique.

*### 6.3 C++

'`cpp
/* Leetcode 3546 – Partage de la grille de somme égale Les
Mise en œuvre C++17 en utilisant des montants préfixés
*/
solution de classe {
public:
bool canPartitionGrid(vecteur<vecteur<int>>& grille) {
int m = quadrillage.size();
int n = grille[0].taille();
vecteur <long long> rangSum(m, 0), colSum(n, 0);
long total = 0;

// Construisez les montants de ligne et de colonne
pour (int i = 0; i < m; ++i) {
pour (int j = 0; j < n; ++j) {
long vall = grille[i][j];
rowSum[i] += valeur;
C'est la première fois que l'on s'en occupe. valeur;
total += valeur;
}
}

// Coupes horizontales
long long supérieur = 0;
pour (int i = 0; i < m - 1; ++i) {
supérieur += rangSum[i];
si (upper) = total - supérieur) retour vrai;
}

// Coupes verticales
longue gauche = 0;
pour (int j = 0; j < n - 1; ++j) {
gauche += colSum[j];
si (gauche == total - gauche) retourner vrai;
}

retourner faux;
}
};
«» "

> **64-bit entiers** («long long») sont requis pour la même raison que Java «long».

---

- Oui. 7. − Harnais d ' essai (facultatif)

Vous pouvez rapidement vérifier la solution dans n'importe quelle langue:

Javascript
// Java
[] g = {{1,2},{3,4}};
Solution s = nouvelle solution();
System.out.println(s.canPartitionGrid(g)); // false

// Python
print(can_partition_grid([[5,1,1],[1,5]]) # true
«» "

---

- Oui. 7. Le bon, le mauvais et le mauvais

Le bon Le mauvais Le mauvais
- C'est quoi ?
**Limpidité algorithmique**=Les montants du préfixe → O(m + n)=Un grand nombre d'intervieweurs codent toujours la version de l'O(m × n) brute-force parce qu'il s'agit de "quick & sales". Oublier de gérer l'affaire *odd‐total* est un slip-up classique. Autres
**Le choix de la langue**=Java, Python, C++ sont tous superbes sur un CV==L'utilisation de `int` pour les sommes peut conduire à des bogues débordants – les intervieweurs vont repérer cela. Entreposer la grille entière en mémoire quand vous n'avez besoin que de sommes est un gaspillage. Autres
**Manipulation de cas d'Edge**= Les boucles `m-2` et `n-2` sautent naturellement les coupures impossibles== Le fait de manquer les limites `-1` dans la boucle provoque une erreur de hors des limites. Oublier d'utiliser 64 bits entiers casse les tests cachés. Autres
**Readability** Ajouter des impressions de débogage *à l'intérieur* les boucles ruineront les performances. Autres

---

- Oui. 8. Ce que nous avons appris

- **Prefix sums** peut transformer un problème apparemment matriciel en un scan unidimensionnel.
- Utilisez **64-bit entiers** chaque fois que vous additionnez des milliers de nombres qui peuvent être jusqu'à `105`.
- Une bonne réponse à l'entrevue n'est pas juste correcte – c'est *explicable*, *optimisé* et *robust*.

---

- Oui. 9. À emporter final

Si vous pouvez marcher un intervieweur à travers ce problème avec:

1. L'observation intuitive** (préfixation des montants de la ligne/colonne)
2. Diagramme d ' algorithme clair **O(m + n)**
3. Une brève analyse de l'espace-temps**
4. Manipulation de tous les cas bord

vous allez démontrer que vous n'êtes pas seulement un codeur, vous êtes un *problème-solveur*.

---

- Oui. 10. Lire plus

- **Codage à gauche 3546**: [Problème sur le Leetcode](https://leetcode.com/problèmes/equal-sum-grid-partition-i/)
- **Préfixer les montants en 2-D** : <https://www.geeksforgeeks.org/2d-prefix-sum/>
- **Problèmes de matrice de style d'entrevue**: <https://www.indeed.com/career-advice/interviewing/2d-array-problèmes>

Bonne chance, et que votre prochaine entrevue soit aussi douce que cette solution!