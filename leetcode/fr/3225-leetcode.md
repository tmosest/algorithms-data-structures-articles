---
titre: LeetCode 3225. Score maximum des opérations de la grille -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

♪ **Score maximal des opérations de grille (Code de débit 3225) – Une plongée profonde**

> *Hard – 5 – 100 × 100 grille – DP + récursion – temps O(n3), espace O(n3)*

> **Mots clés** – LeetCode, Programmation dynamique, Java, Python, C++, Interview, Opérations de grille, Codage Interview, Résolution de problèmes, Interview d'emploi, Algorithme Analyse

---

- Oui. 1. Exposé des problèmes

On vous donne une matrice `n × n` `grid`.
Toutes les cellules sont initialement **blanc**.

**Opération**
Choisir une cellule `(i , j)` et peindre **noir** chaque cellule de la colonne `j` de la ligne `0` jusqu'à la ligne `i` (inclus).

**Note**
Pour chaque cellule *blanc* qui a une cellule **horizontale noire** adjacente (à sa gauche ou à sa droite), vous gagnez `grid[i][j]`.
Le score de toute la grille est la somme de toutes ces valeurs gagnées.

> **Objectif** – Effectuer n'importe quel nombre d'opérations pour maximiser le score.

---

- Oui. 2. Pourquoi est-ce difficile?

Autres Ce qui le rend difficile
C'est ce qu'on dit.
**La plus grande plage de valeurs**= `grid[i][j]` peut être jusqu'à `109`, de sorte que la réponse ne correspond pas à un entier 32 bits. Autres
**État complexe** Chaque colonne peut être partiellement peinte; l'impact futur dépend du nombre de lignes déjà peintes dans les colonnes précédentes. Autres
**L'interdépendance entre les colonnes**La peinture d'une cellule dans la colonne `j` peut affecter la possibilité de peindre des cellules dans la colonne `j+1` (car une cellule noire bloque une cellule blanche). Autres
**Recherche naïve exponentielle**= Chaque colonne a des possibilités `n+1` (peinture 0 ... n lignes). La force brute serait `O(n+1)^n)` – impossible pour `n = 100`. Autres

La solution acceptée utilise la programmation **dynamique** avec un état tridimensionnel qui capture exactement l'information nécessaire pour des sous-problèmes optimaux.

---

- Oui. 3. Intuition et conception de l'État

Voyons les colonnes de **de gauche à droite**.

Lorsque nous sommes à la colonne `c`, nous savons déjà:

1. ** `dernier1`** – le nombre de lignes peintes **par colonne `c-1`**.
Cela nous indique quelles lignes sont déjà noires au *start* de la colonne `c`.

2. ** `dernier2`** – le nombre de lignes peintes **par colonne `c-2`**.
Cela est important car une cellule noire de la colonne `c-2` peut bloquer une cellule blanche de la colonne `c-1`, qui peut à son tour bloquer une cellule blanche de la colonne `c`.

Avec ces deux chiffres, nous pouvons calculer la contribution de la colonne `c` pour tout choix que nous faisons dans cette colonne:

* **Case I – Ne pas peindre quoi que ce soit dans la colonne `c`**
Nous ne gardons que les lignes qui étaient déjà noires de `dernier2`.

* **Case II – Peignez quelques lignes dans la colonne `c` et **bloc** «c+1»**
Si nous peignons des lignes commençant de `last1` à `i`, nous devons définir `last1` pour la colonne suivante à `i+1` et `last2` à `0` (parce que les lignes de `last1` seront noires et ne seront plus disponibles pour la colonne `c+1`).

* **Case III – Lignes de peinture dans la colonne `c` mais **ne bloquez pas la colonne** «c+1»**
Nous gardons les rangées de `last2` et peignons toutes les rangées de `last2` vers le bas.
Pour la colonne suivante, `last1` devient `0` et `last2` devient le nouveau nombre peint.

Cela conduit à la récurrence du PDD :

«» "
dp[col][last1][last2] = score maximal à partir de la colonne col
«» "

La transition énumère tous les choix possibles pour la colonne actuelle (cas I, II, III) et reprend dans la colonne suivante, en gardant la trace des nouveaux "dernier1" et "dernier2".

---

- Oui. 4. Complexité

* **Heure** – «O(n3)»
Pour chaque colonne (`n`) nous itérer au-dessus de `dernier1` (`- n`) et `dernier2` (`- n`). À l'intérieur, nous tournons de nouveau au-dessus des rangées (`- n`).
* **Espace** – `O(n3)` pour mémorisation (peut être réduit à `O(n2)` si vous ne gardez que deux couches, mais la table tridimensionnelle simple est plus facile à comprendre).
* ** Taille de la réponse** – Utiliser des entiers 64 bits (`long`/`int64_t`/`int` en Python).

---

- Oui. 5. Mise en oeuvre des références

Voici des implémentations propres et bien commentées dans **Java**, **Python** et **C++**.

---

#### 5.1 Java (PDD récursif avec mémoisation)

"Java
Importation de java.util.*;

solution de classe publique {
// table de mémorisation
mémoire privé Long[][];
grille privée int[];
Int. privé n;

public long maximum Score(int[][] grille) {
Ça. grille = grille;
c.n = longueur de la grille;
// +1 parce que last1 / last2 peut être égal à n (peinture toutes les lignes)
mémo = nouveau Long[n + 1][n + 1][n + 1];
retour dfs(0, 0, 0);
}

/** @param col colonne courante (0-basée)
* @param dernières1 lignes peintes par colonne col‐1
* @param last2 lignes peintes par colonne col‐2
*/
long dfs (int col, int last1, int last2) {
si (col == n) retourner 0; // terminé toutes les colonnes
si [memo[col][last1][last2] != nul]
retour du mémo[col][dernier][dernier2];

longue meilleure = 0;

/* ---- Cas I : ne pas peindre cette colonne ---- */
long deLast2 = 0;
pour (int r = 0; r < last2; r++) deLast2 += grid[r][col];
best = Math.max (best,
deLast2 + dfs(col + 1, 0, last1);

/* ---- Cas II : peindre quelques lignes, bloquer la colonne suivante ---- */
somme longue = 0;
si (col + 1 < n) {
pour (int r = last1; r < n; r++) {
la somme += grille[r][col];
best = Math.max (best,
la somme + dfs(col + 1, r + 1, 0);
}
}

/* ---- Cas III : lignes de peinture mais ne bloque pas la colonne suivante ---- */
durée longue = 0;
pour (int r = 0; r < n; r++) {
si (r < last2) temp -= grille[r][col];
best = Math.max (best,
température + dfs (col + 1, 0, r + 1);
}

mémo[col][dernier1][dernier2] = meilleur;
le meilleur retour;
}

public statique vide principal(String[] args) {
Solution s = nouvelle solution();
[] g = {
{0,00,00,0},
{0,0,3,0,0},
[0,1,0,0,0,0],
[5,0,0,0,0],
[0,0,0,2]
};
Système.out.println(s.maximumScore(g)); // 11
}
}
«» "

---

#### 5.2 Python (Récursion + `functools.lru_cache`)

'`python
à partir de functools importer lru_cache
de taper l'importation Liste

Solution de classe:
def maximum Note(même, grille: Liste[Liste[int]]) -> Int:
n = len(grid)

@lru_cache(maxsize=Aucune)
def dfs(col: int, last1: int, last2: int) -> Int:
si col == n:
retour 0

- Oui. Case I: sauter cette colonne
de_last2 = somme(grid[r][col] pour r dans l'intervalle(last2))
best = de_last2 + dfs(col + 1, 0, last1)

- Oui. Cas II: lignes de peinture, bloc colonne suivante
somme_ = 0
si col + 1 < n:
pour r dans la plage (dernière année), n:
Sum_ += grille[r][col]
best = max(meilleur, somme_ + dfs(col + 1, r + 1, 0))

- Oui. Cas III: lignes de peinture, mais garder la colonne suivante ouverte
durée = 0
pour r dans la plage(n):
si r < last2:
temp -= grille[r][col]
best = max(meilleur, température + dfs(col + 1, 0, r + 1))

le meilleur retour

retour dfs(0, 0, 0)

♪ Essai de prélèvement
si __nom__ == "__main__" :
s = Solution()
g = [
[0,0,0,0],
[0,0,3,0,0],
[0,1,0,0],
[5,0,0,0],
[0,00,2]
- Oui.
print(s.maximumScore(g)) # 11
«» "

---

### 5.3 C++ (Top-Down DP avec mémoisation)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long long maximum Score(vecteur<vecteur<int>>& grille) {
n = taille de la grille();
ce->grid = &grid;
mémo.assign(n + 1, vector<vector<long long>>(n + 1, vector<long long>(n + 1, LLONG_MIN));
retour dfs(0, 0, 0);
}

particulier:
l'élément n;
grille vectorielle<vector<int>>*;
vecteur<vecteur<vecteur<vecteur<long>>> mémo;

long long dfs(int col, int last1, int last2) {
si (col == n) retourner 0;
si [memo[col][last1][last2] != LLONG_MIN) retourner mémo[col][dernier1[dernier2];

longue longue meilleure = 0;

// Cas I: colonne saut
long deLast2 = 0;
pour (int r = 0; r < last2; ++r) deLast2 += (*grid)[r][col];
best = max(best, fromLast2 + dfs(col + 1, 0, last1));

// Cas II: lignes de peinture, bloc colonne suivante
somme longue = 0;
si (col + 1 < n) {
pour (int r = last1; r < n; ++r) {
somme += (*grid)[r][col];
best = max(meilleur, somme + dfs(col + 1, r + 1, 0);
}
}

// Cas III: lignes de peinture, garder la colonne suivante ouverte
durée longue = 0;
pour (int r = 0; r < n; ++r) {
si (r < last2) temp -= (*grid)[r][col];
best = max(meilleur, température + dfs(col + 1, 0, r + 1));
}

mémo[col][dernier1][dernier2] = meilleur;
le meilleur retour;
}
};

// Exemple d'utilisation
Int main() {
Solution s;
vecteur<vector<int>> g = {
{0,00,00,0},
{0,0,3,0,0},
[0,1,0,0,0,0],
[5,0,0,0,0],
[0,0,0,2]
};
<< s.maximumScore(g) << endl; // 11
}
«» "

---

- Oui. 6. Bonnes solutions contre mauvaises solutions – Liste de contrôle

Une bonne solution ?
C'est ce qu'on dit.
**La réponse 64-bits des mains?**=="long` in Java, `long` in C++, `int` in Python. Autres
**Runs dans le temps sur n=100?** Autres
**Mémorise correctement?**=== Tableau 3-dimensionnel ou `lru_cache`. Autres
**Evite le débordement d'entiers?**** Autres
**Suivez la récurrence du PDD de façon nette?****** Autres
**Le code est-il bien commenté?**=== Les commentaires en ligne aident à la lisibilité. Autres

Si l'un des éléments ci-dessus manque, la solution peut être **mauvais** (par exemple, en utilisant `int` en Java, ou une mémoisation manquante conduisant à un temps exponentiel).

---

- Oui. 7. Essais et cas de bord

Autres Taille de la grille
- C'est quoi ?
Autres `1x1`= Grille minimale== Réponse égale la grille[0]===
Tous les zéros Résultats
Le résultat est égal à la somme totale de toutes les cellules
`n = 100` avec des valeurs aléatoires.
"n = 50" mais valeurs proches de "109" Le risque de débordement est de 64 bits

Testez ceux-ci avec de petits scripts pour garantir l'exactitude avant de soumettre.

---

- Oui. 8. Qu'est-ce qui fait une solution *Bonne*?

Une solution satisfaisante pour ce problème :

1. **Récapituler l'état exact** nécessaire pour les sous-problèmes optimaux (ici: «col, last1, last2»).
2. **Énumérer tous les choix valides** (cas I/II/III) sans double emploi.
3. **Mémoriser** les résultats pour éviter une recomputation.
4. **Poignez de grands nombres** en utilisant des entiers 64 bits.
5. **Restez dans les limites du temps/de l'espace** ('O(n3)').
6. **Soyez facile à lire** – utilisez des noms de variables descriptives et des commentaires.

---

- Oui. 9. A emporter et leçons pratiques

* **3 dimensions DP** peut sembler lourd, mais c'est souvent la *bonne* façon d'encoder les dépendances qui s'étendent sur plus d'une étape (ici, `last1` et `last2').
* ** La mémoisation** peut être implémentée dans de nombreuses langues : récursion + `lru_cache` dans Python, `@lru_cache` ou tables manuelles dans Java/C++.
* ** Analyse de complexité** : Toujours confirmer que la récurrence du PDD réduit la taille du problème.
* **Clarté du code**: Une implémentation propre (comme indiqué ci-dessus) est plus précieuse dans les interviews et sur les systèmes de production qu'une version hautement optimisée mais opaque.

---

## 10. Mot final

La programmation dynamique est une technique *puissante* qui transforme une explosion combinatoire par ailleurs insoluble en une solution polynôme-temps.
En étudiant attentivement l'interaction entre les colonnes de ce problème, nous avons élaboré un PDD tridimensionnel qui saisit exactement l'information nécessaire pour prendre des décisions optimales.

Si vous vous préparez à des interviews techniques, la maîtrise de ce type de design d'état vous aidera à résoudre de nombreux problèmes de "grid-peinture" ou de "blocage" qui apparaissent dans les concours ou les systèmes du monde réel.

Bon codage ! C'est ce qu'il a dit.

---

**Les étiquettes de recherche**: #Java #Python #C++ #Programmation Dynamique #LeetCode #InterviewQuestion #DPStateDesign #64bitentier #Mémoisation
---
*Posté le 2024‐03‐18 par -
---
*Si vous avez aimé ce post, envisagez de vous abonner à des tutoriels DP et algorithme plus propres. *
---
*Sentez-vous libre d'ouvrir les problèmes si vous remarquez des bugs ou voulez des optimisations. *