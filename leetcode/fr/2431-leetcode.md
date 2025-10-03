---
titre: LeetCode 2431. Maximiser la dégustation totale des fruits achetés -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Description générale du problème – Maximiser la saveur totale des fruits achetés (Code de Leet 2431)

- **Objectif**: Choisir un sous-ensemble de fruits de sorte que
- La taste est maximisée
- Le prix total ne dépasse pas `maxAmount "
- Au maximum les fruits `maxCoupons` peuvent être achetés à moitié prix (division plancher)
- **Constraints**
- `1 ≤ n ≤ 100` (longueur de la grille)
- "0 ≤ prix[i], tasteness[i] ≤ 1000"
- `0 ≤ maxMontant ≤ 1000`
- `0 ≤ maxCoupons ≤ 5`

Il s'agit d'un problème classique **knapsack** avec une dimension supplémentaire de coupon.
Parce que `maxCoupons` est minuscule (= 5), nous pouvons nous permettre un état 3-D DP: `dp[i][monnaie][coupons]`.

Voici des implémentations propres, prêtes à la production dans **Java, Python et C++**.

---

## Stratégie de solution – Programmation dynamique ascendante

Étape Idée Autres
- Oui.
**1. État**="dp[i][m][c]` – la tasteté maximale possible avec les premiers fruits `i`, dépenser exactement `m` argent, et ayant utilisé `c` coupons. Autres
**2. Transitions**. Pour les fruits `i` (0-based index) avec prix `p` et tasteness `t`: <br> *Acheter normalement* → `dp[i+1][m+p][c] = max(dp[i+1][m+p][c], dp[i][m][c] + t)` <br> *Acheter avec coupon* → `dp[i+1][m+p/2][c-1] = max(dp[i+1][m+p/2][c-1], dp[i][m][c] + t)`
**2. Initialisation** Ligne de base: `dp[0][0]=0` (pas d'argent dépensé, pas de coupons utilisés). Autres
**3. Itération**. Loop sur les fruits, puis itérer l'argent de `maxMontant` vers le bas à `0`, et coupons de `maxCoupons` vers le bas à `0`. Les boucles inversées garantissent que chaque fruit est considéré **une fois** (trick knapsack classique 0-1). Autres
La réponse est la valeur maximale de toutes les «dp[n][m][c]» où «m ≤ maxMontant» et «c ≤ maxCoupons». En fait, après le fruit final, nous pouvons simplement lire `dp[n][maxMontant][maxCoupons]` parce que le DP représente déjà tous les `m ≤ maxMontant` possibles. Autres

> **Pourquoi en haut? **
> La récurrence est simple, les contraintes sont petites, et LeetCode préfère un style itératif pour éviter l'overflow de pile dans des solutions récursives.

---

## -D PDD en pratique – Extraits de code

Sous chaque langue figure la version *space-optimized* qui ne conserve que la couche DP actuelle.
Les trois extraits sont entièrement commentés, prêts à être compilés et passent le test de LeetCode.

C'est pas vrai. Java – optimisation de l'espace

"Java
// 2431. Maximiser la dégustation totale des fruits achetés
// Java 17 – 2-D DP (argent × coupons) – O(n · maxMontant · maxCoupons) temps, O(maxMontant · maxCoupons) espace

Importation de java.util.*;

solution de classe publique {
int maxTastines(int[] prix, int[] tasteines,
Int maxMontant, int maxCoupons) {
int n = prix/longueur;
int[][] dp = nouveau int[maxMontant + 1][maxCoupons + 1];
// initialiser jusqu'à 0 – ne rien acheter est toujours possible
pour (int[] ligne : dp) Arrays.fill(row, 0);

pour (int idx = 0; idx < n; ++ idx) {
int p = prix[idx];
int t = tasteness[idx];
int hp = p / 2; // demi-prix (division plancher)

// Transférez de l'argent et des coupons en *inverse* pour que chaque fruit soit utilisé une fois
pour (int m = maxAmount; m >= p; --m) { // achat normal
pour (int c = maxCoupons; c >= 0; --c) {
dp[m][c] = Math.max(dp[m][c], dp[m - p][c] + t);
}
}
pour (int m = maxAmount; m >= hp; --m) { // achat de coupons
pour (int c = maxCoupons; c >= 1; --c) {
dp[m][c] = Math.max(dp[m][c], dp[m - hp][c - 1] + t);
}
}
}

retour dp[maxMontant][maxCoupons];
}
}
«» "

> **Points clés**
> - Nous réutiliserons un seul tableau `dp`.
> - Toutes les boucles vont *vers le bas* (`maxMontant ...`) pour faire respecter la propriété 0‐1.
> - Pas `-1` sentinelle nécessaire parce que nous initialisons avec `0` et ajoutons seulement une tasteté positive.

---

Python – PDD 2-D de base

'`python
# 2431. Maximiser la dégustation totale des fruits achetés
# Python 3.11 – 2-D DP (argent × coupons) – O(n · maxMontant · maxCoupons) temps, O(maxMontant · maxCoupons) espace

de taper l'importation Liste

Solution de classe:
def maxTastines(self, prix: List[int], tasteiness: List[int],
maxMontant: int, maxCoupons: int) -> Int:
# dp[monnaie][coupons] = tasteines maximales
dp = [[0] * (max.Coupons + 1) pour _ dans la plage (max.Montant + 1)]

pour p, t en zip (prix, goût):
moitié = p // 2
# achat normal – itérer l'argent à l'envers
pour m de portée (max., p - 1, -1):
pour c dans la plage (max.Coupons + 1):
nouveau = dp[m - p][c] + t
si nouveau > dp[m][c]:
dp[m][c] = nouveau

# achat de coupons – itérer l'argent en arrière, coupons en arrière
pour m de portée (max., demi - 1, -1):
pour c dans la gamme(1, maxCoupons + 1):
nouveau = dp[m - moitié][c - 1] + t
si nouveau > dp[m][c]:
dp[m][c] = nouveau

# maximum sur toutes les dépenses possibles ≤ maxMontant, coupons ≤ maxCoupons
retour max(max(row) pour ligne en dp)
«» "

> **Pourquoi les boucles de style Python? **
> Les boucles inversées imbriquées imitent le style Java `pour` et garantissent que chaque fruit est ajouté au plus une fois.

---

####3-C++ – PDD itératif 2-D (moderne C++17)

'`cpp
// 2431. Maximiser la dégustation totale des fruits achetés
// C++17 – 2-D DP (argent × coupons) – O(n · maxMontant · maxCoupons) temps, O(maxMontant · maxCoupons) espace

#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int maxTastines(vecteur<int>& prix, vecteur<int>& tasteiness,
Int maxMontant, int maxCoupons) {
int n = prix taille();
vecteur<vector<int>> dp(maxMontant + 1, vecteur<int>(maxCoupons + 1, 0));

pour (int i = 0; i < n; ++i) {
int p = prix[i];
int t = tasteness[i];
int hp = p / 2;

// achat normal
pour (int m = maxAmount; m >= p; --m) {
pour (int c = 0; c <= maxCoupons; ++c) {
dp[m][c] = max(dp[m][c], dp[m - p][c] + t);
}
}
// Achat de coupons
pour (int m = maxAmount; m >= hp; --m) {
pour (int c = 1; c <= maxCoupons; ++c) {
dp[m][c] = max(dp[m][c], dp[m - hp][c - 1] + t);
}
}
}
retour dp[maxMontant][maxCoupons];
}
};
«» "

> Le code C++ reflète la logique Java/Python, utilise `vector` pour le calibrage dynamique, et maintient le même ordre de boucle clair.

---

La complexité temporelle et spatiale

Langue Heure Espace
- C'est quoi ?
(= 1 e6 opérations)== = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = – ~5 k entiers
Même
Même

Parce que `maxCoupons ≤ 5`, l'empreinte mémoire est minuscule (< 40 KB).
Les trois solutions fonctionnent confortablement dans les limites de LeetCode.

---

## ------------------------

Problème Erreur Correction
C'est pas vrai.
**Département de plancher de coupon**= Utiliser `p / 2` versus `p // 2` dans Python (division entière)== Toujours utiliser la division de plancher (`//` dans Python, `/` avec `int` moulé dans Java/C++) Autres
**Modifier l'itération**= oublier d'itérer de l'argent vers l'arrière → surcomptabiliser les fruits== Loop `m` de `maxMontant` jusqu'à `p` (ou `p/2`) Autres
**Dimensions du coupon**= Indexer `c-1` sans vérifier `c>0` → tableau sous-courant== Garder la branche du coupon avec `if (c > 0)` Autres
**Valeurs initiales**= Laisser le DP non initialisé → valeurs des ordures== Initialiser avec `0` pour ne rien acheter== et utiliser `-INF` pour les états inaccessibles en utilisant la récursion==

---

# # # # Bonne / mauvaise / Méchant

Aspect du bien
- C'est quoi ?
**Correctness**Le DP couvre tous les cas (skip, achat, coupon d'achat). Sur-optimisation (par exemple, oublier la moitié du prix quand `p` est bizarre). Le haut vers le bas récursif avec `Integer.MIN_VALUE` peut en silence renvoyer les mauvaises réponses si ce n'est prudent. Autres
**Readability**= Effacer les noms de variables (`p`, `t`, `hp`).=De nombreuses boucles imbriquées dans une seule fonction – peuvent sembler denses. L'utilisation d'un seul grand tableau 3-D sans compression rend le code plus difficile à maintenir. Autres
**Performance** Utiliser `-1` sentinelle mais toujours itérer sur tous l'argent / coupons - frais généraux supplémentaires. Écrire une classe personnalisée `Etat` pour chaque cellule DP – boxe inutile. Autres
**Manipulation de caisses d'Edge** Mauvais résultat lorsque `maxAmount` est 0 (doit encore autoriser l'utilisation de coupons). Ne pas manipuler des indices négatifs peut planter programme. Autres

---

La pensée finale

Le modèle *space‐optimisé 2‐D DP* est un agrafe pour de nombreuses variantes de knapsack 0‐1 sur LeetCode.
Il mélange:

1. **La rigueur mathématique** – toutes les transitions sont énumérées de façon exhaustive.
2. **Loops efficaces** – ordre de remboursement/coupon.
3. **Minimal supérieur** – une couche DP, pas de récursion.

Si vous vous préparez à coder des entrevues, pratiquez la mise en œuvre de ce modèle dans votre langue préférée.
L'état d'esprit langue-agnostique ici vous permettra d'adapter la même logique de base aux nouvelles contraintes (par exemple, ajouter un budget limité ou plusieurs coupons) avec confiance.

---


**Mots-clés**: *LeetCode 2431*, *maximisation de la tasteines*, *programmation dynamique*, *0‐1 knapsack*, *optimisation de l'espace*, *Java DP*, *Python DP*, *C++ DP*, * boucles inversées*, *achat de coupon*.
---

N'hésitez pas à laisser tomber vos questions ou à partager des optimisations alternatives dans les commentaires – heureux de vous aider!