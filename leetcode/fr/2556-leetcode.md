---
titre: LeetCode 2556. Déconnecter le sentier dans une matrice binaire par au plus un Flip -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 2556 – Déconnecter Path in a Binary Matrix by at Most One Flip
- Oui. Résolvez-le en Java, Python et C++ – et apprenez le bon, le mauvais et le laid

---

Aperçu du problème

On vous donne une matrice binaire `grid` (taille *m × n*, `1 ≤ m, n ≤ 1000`, `m·n ≤ 105`).
De n'importe quelle cellule `(r, c)` vous pouvez déplacer **right** ou **down** vers une cellule voisine qui contient `1`.
Le départ est `(0,0)` et le but est `(m-1, n-1)` – les deux sont garantis «1».

Vous pouvez **déplier la valeur d'au plus une cellule** (à l'exclusion des deux paramètres).
Flipper les modifications `0 → 1` ou `1 → 0`.

> **Retour `true` si vous pouvez faire la matrice déconnectée** (c'est-à-dire qu'il n'y a pas de chemin du début au but après au plus un flip), sinon `false`.

---

## C'est clair – Cutting a Path

Parce que les mouvements ne sont qu'à droite ou à bas, le graphique est un graphique acyclique ** dirigé (DAG)**.
Une cellule `v` est une cellule *critique* si **chaque** chemin du début au but passe par `v`.
Décoller une telle cellule de `1 → 0` détruit immédiatement tous les chemins.

Ainsi le problème se réduit à:
**Y a-t-il une cellule "v " (0,0),(m-1,n-1)" qui est sur tous les chemins ? * *

Nous pouvons y répondre par une programmation dynamique :

* `dp1[i][j]` – nombre de façons d'atteindre la cellule `(i,j)` dès le début.
* `dp2[i][j]` – nombre de façons d'atteindre l'objectif à partir de la cellule `(i,j)`.

Si le nombre total de chemins est `P = dp1[m-1][n-1]`, alors une cellule `(i,j)` est critique sif

«» "
Dp1[i][j] > 0 ET dp2[i][j] > 0 ET dp1[i][j] * dp2[i][j] == P
«» "

Le produit compte exactement les chemins qui traversent cette cellule – si elle est égale à `P`, **all** chemins doivent passer par elle.

---

Aperçu de la solution

1. **Early exit** – si `P == 0`, la matrice est déjà déconnectée → retourner `true`.
2. Calculer `dp1` (de haut en bas, de gauche à droite).
3. Calculer `dp2` (de bas en haut, de droite à gauche).
4. Scanner toutes les cellules (sauf les paramètres).
Si l'un d'eux satisfait à la condition ci-dessus, retourner `true`.
5. Sinon, retournez "faux".

L'algorithme fonctionne en temps **O(m·n)** et utilise la mémoire **O(m·n)**.
Comme le nombre de chemins peut être astronomique, nous utilisons des entiers de précision arbitraires:
* **Java** – Java.math. Grand entier "
* **Python** – intégré "
* **C++** – `boost::multiprecision::cpp_int "

---

Mise en œuvre du code

- Oui. 1. Java

"Java
importation java.math. BigIntégre;
Importation de java.util.*;

solution de classe {
booléen public estpossibleToCutPath(int[][] grille) {
int m = longueur de grille, n = longueur de grille[0];
BigInteger[][] dp1 = nouveau BigInteger[m][n];
BigInteger[][] dp2 = nouveau BigInteger[m][n];

// dp1 – chemins du début à (i,j)
pour (int i = 0; i < m; ++i) {
pour (int j = 0; j < n; ++j) {
si [grid[i][j]] 0) {
dp1[i][j] = BigInteger. ZÉRO;
poursuivre;
}
Top BigInteger = (i > 0) ? dp1[i-1][j] : Grand entier. ZÉRO;
BigInteger gauche = (j > 0) ? dp1[i][j-1] : Grand entier. ZÉRO;
Dp1[i][j] = (i] 0 && j == 0) ? BigInteger.ONE : haut.add (à gauche);
}
}

Total BigInteger = dp1[m-1][n-1];
i (total.égal(BigInteger. ZERO)) retour true; // déjà déconnecté

// dp2 – chemins de (i,j) à but
pour (int i = m-1; i >= 0; --i) {
pour (int j = n-1; j >= 0; --j) {
si [grid[i][j]] 0) {
dp2[i][j] = Biginteger. ZÉRO;
poursuivre;
}
Bas BigInteger = (i+1 < m) ? dp2[i+1][j] : Grand entier. ZÉRO;
BigInteger droite = (j+1 < n) ? dp2[i][j+1] : Grand entier. ZÉRO;
dp2[i][j] = (i] m-1 && j == n-1) ? BigInteger.ONE : bas.add(à droite);
}
}

// vérifier chaque cellule interne 1
pour (int i = 0; i < m; ++i) {
pour (int j = 0; j < n; ++j) {
si (i=0 && j=0)=1 (i=m-1 && j=n-1) continue;
si [grid[i][j]] 0) continuer; // seulement 1-cellules peuvent être coupées
BigInteger à travers = dp1[i][j].multiply(dp2[i][j];
si (par.equals(total)) retourne vrai;
}
}
retourner faux;
}
}
«» "

---

- Oui. 2. Python

'`python
Solution de classe:
def isPossibleToCutPath(self, grid: List[List[int]]) -> bool:
m, n = len(grid), len(grid[0])
dp1 = [[0]*n pour _ dans la plage(m)]
dp2 = [[0]*n pour _ dans la plage(m)]

# dp1
pour i dans la plage (m):
pour j dans la plage(n):
si grille[i][j]] 0:
dp1[i][j] = 0
poursuivre
Si i == 0 et j == 0:
dp1[i][j] = 1
Sinon:
dp1[i][j] = (dp1[i-1][j] si i>0 autre 0) + (dp1[i][j-1] si j>0 autre 0)

Total = dp1[m-1][n-1]
si total == 0:
retour Vrai # déjà déconnecté

# dp2
pour i dans la plage (m-1, -1, -1):
pour j dans la plage (n-1, -1, -1):
si grille[i][j]] 0:
dp2[i][j] = 0
poursuivre
Si i == m-1 et j == n-1:
dp2[i][j] = 1
Sinon:
dp2[i][j] = (dp2[i+1][j] si i+1<m autre 0) + (dp2[i][j+1] si j+1<n autre 0)

pour i dans la plage (m):
pour j dans la plage(n):
i (i==0 et j==0) ou (i==m-1 et j==n-1):
poursuivre
if grid[i][j]==1 et dp1[i][j]*dp2[i][j]== Total général
retour Vrai
Retour Faux
«» "

---

- Oui. 3. C++

'`cpp
#incluez <bits/stdc++.h>
#incluez <boost/multiprecision/cpp_int.hpp>
utilisant l'espace de noms std;
utilisant boost::multiprecision::cpp_int;

solution de classe {
public:
bool isPossibleToCutPath(vecteur<vector<int>& grille) {
int m = quadrillage(), n = quadrillage[0].size();
vector<vector<cpp_int>> dp1(m, vector<cpp_int>(n));
vector<vector<cpp_int>> dp2(m, vector<cpp_int>(n));

// dp1 – du début à (i,j)
pour (int i=0;i<m;i++){
pour (int j=0;j<n;j++){
si (grid[i][j]==0){ dp1[i][j]=0; continuer; }
cpp_int top = (i>0)?dp1[i-1][j]:0;
cpp_int gauche = (j>0)?dp1[i][j-1]:0;
dp1[i][j] = (i==0 && j==0)?1:top+gauche;
}
}

cpp_int total = dp1[m-1][n-1];
si (total==0) retourne true; // déjà déconnecté

// dp2 – de (i,j) au but
pour (int i=m-1;i>=0;i--) {
pour (int j=n-1;j>=0;j--) {
si (grid[i][j]==0){ dp2[i][j]=0; continuer; }
cpp_int down = (i+1<m)?dp2[i+1][j]:0;
cpp_int right= (j+1<n)?dp2[i][j+1]:0;
Dp2[i][j] = (i==m-1 && j==n-1)? 1: vers le bas+à droite;
}
}

pour (int i=0;i<m;i++){
pour (int j=0;j<n;j++){
si ((i=0 && j=0)=" (i=m-1 && j=n-1) continue;
si (grid[i][j]==1 && dp1[i][j]*dp2[i][j]==total) retourner vrai;
}
}
retourner faux;
}
};
«» "

> *Astuce*: Si vous ne voulez pas tirer dans Boost, vous pouvez remplacer `cpp_int` par un grand entier personnalisé ou utiliser `std::uint64_t` et le capuchon à une grande valeur sentinelle – la comparaison de produit fonctionne de la même manière.

---

Pourquoi cela compte pour les intervieweurs et les chercheurs d'emploi

1. **Clarité** – L'approche DP est facile à raisonner et est un trick classique de "count-paths".
2. **Échelle** – Poignée la plus mauvaise taille de cas (cellules `105`) en temps linéaire.
3. **Language-agnostique** – La même logique fonctionne en Java, Python et C++.
4. **Show‐case** – Démontre votre capacité à:
* Traduire un point d'articulation graphi-théorique en un problème DP.
* Utilisez l'arithmétique de précision arbitraire au besoin.
* Écrire un code propre et vérifiable.

Si vous préparez une entrevue d'ingénierie logicielle (surtout chez Google, Amazon, Microsoft ou fintech), ce problème est une vitrine parfaite de la pensée algorithmique et de la manipulation soignée des cas.

---

Bon, le mauvais et l'horrible problème

Le bon Le mauvais Le mauvais
- C'est quoi ?
**Structure du graphique**=DAG (à droite/à bas seulement) → aucun cycle → Les mouvements sont *seulement* à droite/à bas → vous ne pouvez pas simplement utiliser des algorithmes point-articulation non dirigé.= Si vous oubliez cette directionnalité et essayez un DFS/BFS aveugle pour chaque cellule, la complexité explose à O((m·n)2). Autres
**Le comptage de la feuille de calcul**= Java `BigInteger`/Python=s `int` donne une précision illimitée. Les chemins de comptage peuvent déborder de 64 bits même pour les petites grilles (par exemple, 30×30 → ~108 chemins). L'utilisation d'entiers 32 bits ou 64 bits peut produire de faux positifs/négatifs. Autres
**Mise en oeuvre**Le DP est simple; deux passes, une dernière analyse. Il faut sauter soigneusement les paramètres – bug facile. Oublier de gérer le boîtier déjà déconnecté (total = 0) peut mener à l'A.O. lors d'un test caché. Autres
Autres **Complexité du temps** Aucun.La naïveté, essai chaque cellule est O((m·n)2) – totalement invraisemblable. Autres
Deux tableaux 2-D de `BigInteger` / `cpp_int`. Si vous préférez enregistrer la mémoire, vous pouvez réutiliser un tableau DP et calculer `dp2` à la volée, mais la comparaison de produits nécessite toujours le deuxième tableau. Autres

---

Que prendre à la maison

1. **Propriété DAG** → DP fonctionne pour compter les chemins.
2. **All-paths-through-a-cell** est un contrôle de produit: `dp1 *dp2 == total`.
3. ** La précision arbitraire** est nécessaire car le nombre de chemins peut exploser.
4. **Début de sortie**: s'il n'y a pas de chemin du tout, vous êtes déjà déconnecté.
5. ** Exclut les paramètres** – ils ne peuvent pas être retournés.

---

Référence rapide – Lignes clés

La langue de la déclaration de Big-Int Mise à jour des cellules DP
-- -- -- -- -- -- -- -- -- -- -- -- -- -- --
Java" "BigInteger[]] dp1 = nouveau BigInteger[m][n];"" dp1[i][j] = top.add(gauche);"" dp1[i][j].multiply(dp2[i][j]).equals(total)" Autres
Python `dp1 = [[0]*n pour _ dans l'intervalle(m)]`= `dp1[i][j] = haut + gauche`= `dp1[i][j] * dp2[i][j]= total`=
C++="vector<vector<cpp_int>> dp1(m, vector<cpp_int>(n));`= `dp1[i][j] = haut + gauche;`= `dp1[i][j] * dp2[i][j]= total"

---

Le dernier Verdict

Ce problème est un mélange soigné de la théorie **graph**, de la programmation **dynamique** et de l'arithmétique **big-integer**. Maîtriser cela signifie que vous pouvez répondre en toute confiance à une large classe de questions sur le nombre de voies dans les entrevues.

Bonne chance, et le codage heureux! C'est ce qu'il a dit.

---