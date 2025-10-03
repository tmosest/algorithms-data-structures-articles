---
titre: LeetCode 3240. Nombre minimum de flips pour rendre Binary Grid Palindromic II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Réponse**

Pour une matrice binaire de taille égale, le problème se divise en groupes 4 cellules indépendants.
Laissez

«» "
(i , j) – coin supérieur gauche du groupe
(i , m-1-j) – coin supérieur droit
(n-1-i , j) – coin inférieur gauche
(n-1-i, m-1-j) – coin inférieur droit
«» "

(Ici `n` est le nombre de lignes et `m` le nombre de colonnes.)

Pour chaque groupe nous pouvons soit faire les quatre cellules 0 ou les quatre cellules 1 –
Les deux choix garantissent que chaque sous-matrix 2×2 a un nombre pair de 1.
Le coût des deux choix est

«» "
cnt = somme des quatre cellules
coûtAllZero = cnt // flip all 1→0
coûtAllOne = 4 - cnt // flip all 0→1
«» "

Par conséquent, le coût minimal pour ce groupe est «min(cnt, 4-cnt)».
L'ajout des coûts sur tous les groupes donne l'optimum global parce que le
les groupes sont disjoints et indépendants.

"Java
solution de classe {
Int public minFlips(int[][] grille) {
int n = longueur de grille, m = longueur de grille[0];
Int ans = 0;
pour (int i = 0; i < n / 2; ++i) {
pour (int j = 0; j < m / 2; ++j) {
int cnt = grille[i][j] + grille[i][m-1-j]
+ grille[n-1-i][j] + grille[n-1-i][m-1-j];
ans += Math.min(cnt, 4 - cnt);
}
}
le retour des an;
}
}
«» "

Donc, ** le nombre minimum de tours est égal à la somme de "min(cnt, 4-cnt)" sur tous les
Groupes de 4 cellules**.
Cette solution fonctionne dans **O(n ·m)** temps et utilise **O(1)** espace supplémentaire.