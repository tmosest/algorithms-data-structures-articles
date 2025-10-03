---
titre: LeetCode 1895. La plus grande place magique -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Le guide complet du LeetCode 1895 – La plus grande place magique
*Les solutions Java, Python & C++ + une plongée profonde

---

Récapitulation des problèmes
> **La plus grande place magique* *
> On vous donne une grille entière `m × n` (`1 ≤ m, n ≤ 50`).
> Un sous-square **k × k** est un carré *magique* si **chaque somme de ligne, chaque somme de colonne et les deux sommes diagonales sont identiques**.
> Les nombres à l'intérieur d'un carré magique ne **pas** doivent être distincts.
> Retournez la longueur latérale `k` du carré magique *le plus grand* qui se trouve à l'intérieur de la grille.

---

- Oui. Pourquoi ce problème est important
- **Interviews:** Beaucoup d'entreprises demandent une variante du carré magique ou du sous-matrix pour tester la programmation dynamique** et **préfixer les sommes**.
- ** Pensée algorithmique :** Vous apprendrez comment réduire une approche O(m2 n2) de force brute à une solution O(m n min(m, n) efficace.
- ** Compétences linguistiques :** La même logique peut être exprimée en Java, Python ou C++ – parfait pour votre portefeuille.

---

Résumé

#'''''''''''''''''''''
- C'est quoi ?
**Contrôler chaque sous-carré** Autres
Autres Il faut maintenir des tableaux 2-D séparés.
**Contrôle de la taille de l'orge**=Stops de vérification des tailles plus petites une fois que l'on trouve une plus grande taille==Compte rendu de boucle supplémentaire==Comparaison des montants diagonaux (mélange `+` / `-`) Autres
Autres *Le choix de la langue *Java/C++ donne la vitesse, Python donne la brièveté *Java a besoin de tailles de tableau explicites *C++ nécessite un pointeur arithmétique prudent *

---

- Oui. La solution efficace – Préfixe sums + recherche de graisse

4.1 Précompensations

Données Formule Objet
- C'est quoi ?
"rowPrefix[i][j]"""rowPrefix[i][j-1] + grid[i][j]"" Somme de la ligne `i` de la colonne 0 à j"
«colPrefix[i][j]»»«colPrefix[i-1][j] + quadrillage[i][j]«» Somme de la colonne «j» de la ligne 0 à «i»

Avec ces deux tableaux nous pouvons obtenir la somme de tout segment horizontal ou vertical en O(1).

4.2 Vérification d'un carré

1. **Somme cible** – utilisez la première ligne (ou colonne) du carré candidat.
2. **Toutes les lignes** – vérifier que chaque somme de lignes est égale à la cible.
3. **Toutes les colonnes** – vérifier que chaque somme de colonne est égale à la cible.
4. **Diagonaux** – calculent directement les principaux et les anti-diagonaux (coût O(k)).
5. Si tous les chèques passent, nous avons trouvé un carré magique de la taille `k`.

4.3 Complexité

- **Précompte**: 'O(m n) "
- ** Boucle principale**: Pour chaque coin supérieur gauche, nous essayons des tailles du plus grand possible jusqu'au meilleur actuel.
Chaque taille vérifie les coûts `O(k)` pour les lignes + `O(k)` pour les colonnes + `O(k)` pour les diagonales = `O(k)`.
Étant donné que "k ≤ min(m, n) ≤ 50", le total reste "O(m n min(m, n)" " - O(125 000)" - bien dans les limites.
- **Espace**: `O(m n)` pour les deux tableaux de préfixes.

---

Code en trois langues

#### 5.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
publique MagicSquare(int[[]] grille) {
int m = longueur de grille, n = longueur de grille[0];

// Préfixer les montants des lignes et des colonnes
int[]] rowPref = nouvelle int[m][n];
int[] colPref = nouvelle int[m][n];

pour (int i = 0; i < m; i++) {
Int rSum = 0;
pour (int j = 0; j < n; j++) {
rSum += la grille [i][j];
lignePref[i][j] = rSum;
}
}

pour (int j = 0; j < n; j++) {
int cSum = 0;
pour (int i = 0; i < m; i++) {
cSum += la grille [i][j];
colPref[i][j] = cSum;
}
}

int best = 1; // Chaque carré 1x1 est magique
pour (int i = 0; i < m; i++) {
pour (int j = 0; j < n; j++) {
int maxSide = Math.min(m - i, n - j);

// Essayez seulement des tailles plus grandes que nous avons déjà trouvé
pour (int k = maxSide; k > best; k--) {
si (isMagic(i, j, k, grille, lignePref, colPref)) {
meilleur = k;
pause; // Pas besoin de vérifier les plus petites tailles en haut à gauche
}
}
}
}
le meilleur retour;
}

booléen privé estMagic(int r, int c, int sz,
nt[], grille, int[], rangPref, int[], colPref

// Somme du segment de première ligne
cible int = lignePref[r][c + sz - 1];
si (c > 0) cible -= lignePref[r][c - 1];

// Vérifiez chaque ligne
pour (int i = 0; i < sz; i++) {
la ligne intSum = la lignePref[r + i][c + sz - 1];
si (c > 0) ligneSum -= lignePref[r + i][c - 1];
si (rowSum != cible) retourner faux;
}

// Vérifiez chaque colonne
pour (int j = 0; j < sz; j++) {
int colSum = colPref[r + sz - 1][c + j];
si (r > 0) colSum -= colPref[r - 1][c + j];
si (colSum != cible) retourner faux;
}

// Diagonale principale
int diag1 = 0;
pour (int k = 0; k < sz; k++) diag1 += grille[r + k][c + k];
si (diag1 != cible) retourner faux;

// Antidiagone
int diag2 = 0;
pour (int k = 0; k < sz; k++)
Diag2 += quadrillage[r + k][c + sz - 1 - k];
retour diag2 == cible;
}
}
«» "

> **Astuce:** Le "rowPref"/"col Les tableaux Pref sont indexés à 0 – attention avec `c > 0` / `r > 0' chèques.

---

5.2 Python

'`python
Solution de classe:
plus MagicSquare(self, grid: List[List[int]]) -> Int:
m, n = len(grid), len(grid[0])

# Préfixer les sommes
row_pref = [[0]*n pour _ dans l'intervalle(m)]
col_pref = [[0]*n pour _ dans l'intervalle(m)]

pour i dans la plage (m):
s = 0
pour j dans la plage(n):
s += grille[i][j]
ligne_pref[i][j] = s

pour j dans la plage(n):
s = 0
pour i dans la plage (m):
s += grille[i][j]
col_pref[i][j] = s

meilleure = 1
pour i dans la plage (m):
pour j dans la plage(n):
max_side = min(m - i, n - j)
# Essayez d'abord des tailles plus grandes
pour sz dans la gamme (max_side, best, -1) :
i self.is_magic(i, j, sz, grid, row_pref, col_pref):
best = sz
pause
le meilleur retour

def is_magic(self, r, c, sz,
quadrillage, ligne_pref, col_pref) -> bool:
# cible = somme de la première ligne
cible = range_pref[r][c + sz - 1]
si c > 0: cible -= range_pref[r][c - 1]

Vérifiez toutes les lignes
pour i dans la plage (r, r + sz):
row_sum = row_pref[i][c + sz - 1]
si c > 0: ligne_sum -= ligne_pref[i][c - 1]
si ligne_sum != cible:
Retour Faux

# Vérifiez toutes les colonnes
pour j dans la plage(c, c + sz):
col_sum = col_pref[r + sz - 1]
si r > 0: col_sum -= col_pref[r - 1][j]
si col_sum != cible:
Retour Faux

# Diagonale principale
diag = somme(grid[r + k][c + k] pour k dans la plage(sz))
Si diag != cible:
Retour Faux

# Anti-diagone
anti = somme(grid[r + k][c + sz - 1 - k] pour k dans la plage(sz)
cible
«» "

> **Note sur le python:** L'utilisation de la compréhension de la liste permet de garder le code court, mais garde un œil sur le débordement entier pour les entrées plus grandes (pas un problème pour les limites données).

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
(vecteur<vecteur<int>>& grille) {
int m = quadrillage(), n = quadrillage[0].size();

// Préfixer les sommes
vecteur<vector<int>> lignePréf(m, vecteur<int>(n));
vector<vector<int>> colPref(m, vector<int>(n));

pour (int i = 0; i < m; ++i) {
Int r = 0;
pour (int j = 0; j < n; ++j) {
r += grille[i][j];
lignePref[i][j] = r;
}
}

pour (int j = 0; j < n; ++j) {
c = 0;
pour (int i = 0; i < m; ++i) {
c += grille[i][j];
colPref[i][j] = c;
}
}

int best = 1;
pour (int r = 0; r < m; ++r) {
pour (int c = 0; c < n; ++c) {
int maxSide = min(m - r, n - c);
pour (int sz = maxSide; sz > best; --sz) {
si (isMagic(r, c, sz, quadrillage, rangPref, colPref)) {
best = sz;
pause; // pas besoin de vérifier les plus petites tailles
}
}
}
}
le meilleur retour;
}

particulier:
le bool isMagic(int r, int c, int sz,
vecteur<vecteur<int>& grille,
vecteur<vecteur<int>>& lignePréf,
vecteur<vector<int>&colPref) {
// Montant cible de la première ligne
cible int = lignePref[r][c + sz - 1];
si (c > 0) cible -= lignePref[r][c - 1];

// Toutes les lignes
pour (int i = 0; i < sz; ++i) {
int sumRow = lignePref[r + i][c + sz - 1];
si (c > 0) sumRow -= rangPref[r + i][c - 1];
si (sumRow != cible) retourner faux;
}

// Toutes les colonnes
pour (int j = 0; j < sz; ++j) {
int sumCol = colPref[r + sz - 1][c + j];
si (r > 0) sommeCol -= colPref[r - 1][c + j];
si (sumCol != cible) retourner faux;
}

// Diagonale principale
int diag1 = 0;
pour (int k = 0; k < sz; ++k) diag1 += grille[r + k][c + k];
si (diag1 != cible) retourner faux;

// Antidiagone
int diag2 = 0;
pour (int k = 0; k < sz; ++k) diag2 += quadrillage[r + k][c + sz - 1 - k];
si (diag2 != cible) retourner faux;

retour vrai;
}
};
«» "

---

Liste de contrôle du débogage (la mauvaise partie)

Qu'est-ce qui arrive?
- Oui.
**Off‐by‐one dans les montants préfixés**= Mauvaises sommes de rangée/colonne== Utiliser les indices basés sur 0 de façon uniforme. Testez d'abord avec une grille 1×1. Autres
**Débordement entier**= Mauvaise comparaison sur de très grandes grilles=LeetCode limite les nombres à 106; utilisez `long` si vous soupçonnez de plus grandes données. Autres
**Diag1 != diag2' même si les sommes correspondent. Autres
Il est essentiel d'essayer la taille `k` plus grande que les lignes/colonnes restantes. Autres

---

Article de blog optimisé du SEO

> **Titre:**
> La maîtrise du LeetCode 1895 – Plus grande Place magique (Java, Python, solutions C++)* *

> **Meta Description:**
> Découvrez la solution la plus efficace pour LeetCode 1895 – La plus grande place magique. Préparez-vous aux interviews avec le code Java, Python et C++ étape par étape. Améliorez votre confiance en code aujourd'hui!

> ** Mots-clés principaux : **
> LeetCode 1895, La plus grande magie Carré, algorithme de somme préfixe, interview de codage, structures de données, tableaux 2D, programmation dynamique, puzzles algorithmiques.

> **Points de vue et contenu :**

«» "
H1: Mastering LeetCode 1895 – Plus grande Place magique
H2: Aperçu du problème
H2: Pourquoi les montants préfixés changent-ils
H3: Comprendre le préfixe 2D
H2: 3 langues, 3 échantillons de codes propres
H3: Java Implementation (avec des extraits de code)
H3: Implémentation de Python (avec extraits de code)
H3: Mise en œuvre C++ (avec extraits de code)
H2: Bugs communs et comment les éviter
H2: Comment ce problème aide votre préparation d'entrevue
H2: Takeaway – La magie de O(n3) avec O(1) Checks
H2: Prêt à répondre aux questions d'entrevue?
«» "

> **Mots-clés suggérés dans l'article:**
> `LeetCode 1895`, `Largest Magic Square`, `prefix sum`, `2D arrays`, `dynamic programming`, `coding interview`, `Java solution`, `Python solution`, `C++ solution`, `algorithmic challenge`, `concurrential programming`.

> ** Liens internes :**
> - Lien vers un tutoriel sur `2D prefix sums`.
> - Lien vers une discussion générale `LeetCode` pour 1895.

> **Appel à l'action:**
> À la fin, inviter les lecteurs à commenter avec leurs propres solutions, ou essayer des problèmes similaires comme **LeetCode 1984 – La plus grande sous-mesure avec des réarrangements** ou **LeetCode 1738 – Compter les éléments correspondant à une condition**.

---

- Oui. Réflexions finales

Vous avez maintenant :

1. Une compréhension claire** de l'énoncé du problème et des contraintes.
2. **Trois solutions prêtes à la production** dans votre langue préférée.
3. Une feuille de tricheur ** pour garder le code à l'épreuve des balles.
4. Un article convivial** pour mettre en valeur votre expertise sur Medium, Dev.to ou votre blog personnel.

> **Déployez votre solution, partagez votre poste et as cette interview de codage! * *

---