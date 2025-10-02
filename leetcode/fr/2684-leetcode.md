---
titre: LeetCode 2684. Nombre maximum de déplacements dans une grille -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
"'''art
importation 'dart:math';

vide principal() {}

solution de classe {
int maxMoves(Liste<Liste<int>> grille) {
m = longueur de la grille;
Int final n = grille[0].longueur;
Liste finale<Liste<int>> dp = Liste.generate(m, (_) => Liste.rempli(n, 0));

pour (int col = n - 2; col >= 0; col-) {
pour (int rang = 0; rang < m; rang++) {
si (ligne > 0 && grid[row][col] < grid[row - 1][col + 1] {
dp[row][col] = max(dp[row][col], dp[row - 1][col + 1] + 1);
}
si (grid[row][col] < grid[row][col + 1]) {
dp[row][col] = max(dp[row][col], dp[row][col + 1] + 1);
}
si (ligne < m - 1 && grid[row][col] < grid[row + 1][col + 1]) {
dp[row][col] = max(dp[row][col], dp[row + 1][col + 1] + 1);
}
}
}

résultat int = 0;
pour (int rang = 0; rang < m; rang++) {
résultat = max(résultat, dp[row][0]);
}
le résultat du retour;
}
}
«» "