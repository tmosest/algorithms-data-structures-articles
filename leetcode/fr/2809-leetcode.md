---
titre: LeetCode 2809. Temps minimum pour faire la somme d'array au maximum x -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Problème**

On vous donne deux tableaux de la même longueur

«» "
nums1[0 ... n-1] – valeurs courantes
nums2[0 ... n-1] – valeurs de croissance
«» "

A chaque seconde `t` le tableau entier `nums1` grandit par son
valeurs correspondantes `nums2` – c'est-à-dire au moment `t "

«» "
valeur[i] = nombres1[i] + t * nombres2[i]
«» "

Pendant toute seconde, vous pouvez **pick un index et définir `nums1[i]` à `0`**.
Une fois qu'il est zéro, la croissance se produit encore, mais la valeur est toujours
`0 + (t–choisi_time) * nums2[i]`.

Votre objectif est de trouver le plus petit nombre de secondes `t`
(«0 ≤ t ≤ n») de telle sorte qu'après application au plus de «t» opérations zéro
la somme de toutes les valeurs est ≤ `x`.
Si cela est impossible retour `-1`.

-----------------------------------------------------------------------------------

C'est vrai. 1. Observations

* Zéroing un élément avec un **large** `nums2[i]` devrait être fait **fin**,
parce que plus tôt vous le zéro le plus de fois sa croissance est ajoutée
à la somme.
Par conséquent, nous trions d'abord les paires `(nums1[i], nums2[i]) "
par l'augmentation des nombres2.

* Pour un nombre fixe d'opérations `t` nous aimerions savoir
** combien nous pouvons réduire la somme** par rapport au cas où nous faisons
Rien.

* Si nous avons déjà considéré les premières paires `i‐1` et que nous voulons toujours
pour utiliser des opérations `j`, nous pouvons:

1. **Ignorer** la «i» – la réduction est «dp[i‐1][j]».
2. **Utiliser** une opération sur la paire «i» – nous utilisons ensuite
Opérations «j‐1» sur les premières paires «i‐1» et dépenses les dernières
opération sur cette paire.
La réduction apportée par cette paire est

«» "
Nombres1[i] // nous avons mis à zéro sa valeur initiale
+ nombres2[i] * j // nous avons supprimé j croissances futures
«» "

* Ces deux options donnent un DP classique en 2 dimensions.

-----------------------------------------------------------------------------------

C'est vrai. 2. Formule PDD

Laissez

«» "
dp[i][j] – réduction maximale possible de la somme
si nous utilisons au maximum j zéro-opérations
parmi les premières paires i (après tri).
«» "

`dp[0][*] = 0` – sans paires nous ne pouvons rien réduire.

Récurrence pour `1 ≤ i ≤ n` et `1 ≤ j ≤ i` :

«» "
sans _i = dp[i-1] [j] // nous ne faisons pas la paire zéro i
avec_i = dp[i-1][j-1] + nombres1[i] + nombres2[i] * j // nous zéro paire i
dp[i][j] = max( sans _i , avec _i )
«» "

Pourquoi `nums2[i] * j`?
Si nous zéro cette paire au moment `j`, sa valeur à ce moment aurait
a été augmenté «j» fois par «nums2[i]».
Il supprime toutes ces futures augmentations **plus**
Valeur originale «nums1[i]».

Après avoir rempli la table, `dp[n][t]` nous indique la réduction *maximum*
nous pouvons atteindre si nous sommes autorisés exactement "t" zéro-opérations.

-----------------------------------------------------------------------------------

C'est vrai. 3. Trouver la réponse

La somme de tous les éléments après "t" secondes **sans** aucun zéro
les opérations

«» "
S(t) = somme(nums1) + somme(nums2) * t
«» "

Si nous utilisons les meilleures réductions données par «dp[n][t]», la somme réelle est

«» "
sum_after_t = S(t) – dp[n][t]
«» "

Nous avons besoin du plus petit `t` tel que `sum_after_t ≤ x`.
Si aucun tel `t` n'existe (c'est-à-dire même avec `t = n` il est toujours > `x`) nous
retour `-1`.

-----------------------------------------------------------------------------------

C'est vrai. 4. Optimisation de la mémoire

Le DP utilise seulement la ligne précédente, donc nous pouvons garder une seule
Tableau 1-dimensionnel et mise à jour de l'arrière vers l'avant:

«» "
int[] dp = nouvelle int[n+1]; // dp[j] = dp[i][j] après avoir terminé la paire i

pour (int i = 1; i <= n; ++i) {
pour (int j = i; j >= 1; --j) {
dp[j] = Math.max(dp[j], dp[j-1] + nombres1[i] + nombres2[i]*j);
}
}
«» "

-----------------------------------------------------------------------------------

C'est vrai. 4. Complexité

*Trier* : 'O(n log n) "
*DP* : temps `O(n2)`, mémoire `O(n)`
*Trouver t* : 'O(n)' heure

-----------------------------------------------------------------------------------

C'est vrai. 5. Mise en œuvre des références

Voici une implémentation Java concise qui suit ce qui précède
procédure.
(Il est équivalent à la solution classique pour LeetCode 2781,
mais écrit de zéro pour la clarté.)

"Java
Importation de java.util.*;

solution de classe publique {
au moinsSecond(int[] nombres1, int[] nombres2, int x) {
int n = nombres1.longueur;

// 1. trier les indices en augmentant les nombres2
Integer[] idx = nouveau Integer[n];
pour (int i = 0; i < n; i++) idx[i] = i;
les tableaux.sort(idx, a, b) -> Integer.compare(nums2[a], nums2[b]);

// 2. préfixer les montants des tableaux originaux
somme longue1 = 0, somme2 = 0;
pour (int i = 0; i < n; i++) {
sum1 += nombres1[i];
sum2 += nombres2[i];
}

// cas trivial
si (somme1 <= x) retourner 0;

// 3. PDD 1-D
int[] dp = nouvelle int[n + 1]; // dp[j] – meilleure réduction avec j ops
pour (int id = 0; id < n; id++) {
int a = nombres1[idx[id]];
int b = nombres2[idx[id]];
// mise à jour de haute j à basse j pour éviter l'écrasement
pour (int j = id + 1; j >= 1; j--) {
int avec = dp[j - 1] + a + b * j;
int sans = dp[j];
dp[j] = Math.max(avec, sans);
}
}

// 4. trouver le minimum t
pour (int t = 0; t <= n; t++) {
long cur = somme1 + somme2 * t - dp[t];
si (cur <= x) retourner t;
}
retour -1; // même avec toutes les opérations n il ne suffit pas
}
}
«» "

-----------------------------------------------------------------------------------

C'est vrai. 4. Pourquoi cela fonctionne

*Trier garantit que chaque fois que nous décidons de zéro une paire à la fois
`j`, toutes les paires avec des "nums2" plus grands seront examinées plus loin dans le DP
et donc nous sommes autorisés à dépenser l'opération sur eux à
plus tard, ce qui est toujours optimal. *

*Le PDD envisage tous les choix possibles d'opérations zéro
Pour chaque paire, "dp[n][t]" est le véritable maximum
réduction possible avec des opérations `t`. *

*Enfin, nous vérifions simplement les sommes résultantes pour `t = 0 ... n`; la première
le temps que nous pouvons atteindre `x` est le nombre minimal de secondes requis. *

-----------------------------------------------------------------------------------

C'est vrai. 5. Note finale

*Si vous préférez une version de sauvegarde de la mémoire, vous pouvez
Tableau 1-dimensionnel comme indiqué ci-dessus – il a toujours besoin de `O(n2)` heure
car chaque élément doit être traité pour chaque `t`.
L'algorithme est facilement porté sur Python ou C++ ; la clé
La récurrence reste la même. *

Bon codage !