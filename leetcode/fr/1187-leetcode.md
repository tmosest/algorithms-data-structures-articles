---
titre: LeetCode 1187. Faire en sorte qu'il augmente strictement -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Faire en sorte qu'il augmente strictement – un guide de solution complet

** Exposé des problèmes* *
On vous donne deux tableaux entiers `arr1` et `arr2`.
Dans une opération, vous pouvez choisir un index `i` dans `arr1` et un index `j` dans `arr2` et remplacer `arr1[i]` par `arr2[j]`.
`arr2` n'est pas modifié – vous pouvez choisir le même élément à partir de `arr2` plusieurs fois.
L'objectif est de faire `arr1` augmenter strictement (`arr1[i] < arr1[i+1]` pour toutes les `i` valides) en utilisant le nombre minimum d'opérations.
Retournez ce nombre minimum ou `-1` si cela est impossible.

---

- Oui. 1. Principales observations

1. **Nous pouvons arrêter tôt** – si les premiers éléments de `arr1` sont déjà en augmentation stricte, nous n'avons peut-être pas besoin de les toucher.
2. **Bon sur le nombre de swaps** – chaque opération change un élément de "arr1".
Nous n'avons jamais besoin de plus d'opérations "len(arr1)" (chaque élément pourrait être remplacé une fois).
De plus, si l'on remplace plus d'éléments `len(arr2)`, les swaps d'extras sont inutiles parce que la seule chose qui compte est la *valeur* que nous avons mise dans, et non l'index dans `arr2'.
Ainsi, la réponse est limitée par "min(len(arr1), len(arr2)")".
3. **Choisir la bonne valeur à partir de `arr2`** –
Si nous décidons de remplacer `arr1[i]`, nous voudrions mettre la valeur *la plus petite* de `arr2` qui est encore plus grande que la dernière valeur du préfixe croissant.
Puisque `arr2` ne change pas, nous pouvons le trier une fois et utiliser la recherche binaire (`higher()`) pour trouver cette valeur rapidement.

---

- Oui. 2. Formule de programmation dynamique

Nous utilisons le tableau DP suivant (ou une version unidimensionnelle) :

«» "
dp[k] = la plus petite valeur possible du dernier élément
de arr1[0 ... cur] après avoir traité les premiers éléments cur+1
et utilisé exactement k swaps au total
«» "

`dp[k]` est `INF` s'il est impossible d'obtenir un préfixe croissant avec des swaps exactement `k`.

**Répétition** (alors qu'elle dépasse "arr1"):

*Let `prev = dp[k]` est la valeur du dernier élément du préfixe avant la position actuelle. *

1. **Ne pas échanger l'élément courant* *
Si `arr1[i] > prev`, nous pouvons garder `arr1[i]`.
Puis la dernière valeur du nouveau préfixe est `arr1[i]` et le nombre de swaps reste «k»:

«» "
new_dp[k] = min( new_dp[k] , arr1[i] )
«» "

2. **Échanger l'élément courant** (seulement si `k > 0`)
Nous avons besoin du plus petit élément de `arr2` qui est plus grand que la dernière valeur du préfixe précédent, c'est-à-dire plus grand que `dp[k-1]` (la dernière valeur *avant* nous utilisons l'échange `k`-th).
Utilisez la recherche binaire sur le trié `arr2` pour obtenir cette valeur `x`.
Si un tel «x» existe:

«» "
new_dp[k] = min( new_dp[k] , x )
«» "

Parce que nous conservons toujours la valeur la plus petite possible, les positions plus tard ont la meilleure chance de continuer à augmenter.

---

2.1 Initialisation

Lorsque nous n'avons traité que le premier élément `arr1[0]`:

«» "
dp[0] = arr1[0] (aucun échange)
dp[k] (k>0) = min( arr1[0] , plus petit élément en arr2 )
«» "

La deuxième ligne dit: si nous avons déjà échangé au moins une fois avant le premier élément,
nous pouvons soit conserver la valeur originale ou mettre la plus petite valeur possible de `arr2`.

---

- Oui. 3. Algorithme (DP unidimensionnel)

Texte
trier arr2
p = min(len(arr1), len(arr2))
INF = un nombre supérieur à toutes les valeurs possibles (par exemple 10**18)

dp = [INF] * (p+1)
dp[0] = arr1[0]
pour k dans 1..p: # utiliser au moins un swap sur le premier élément
dp[k] = min(arr1[0], arr2[0]) # arr2 est trié, arr2[0] est l'élément le plus petit

pour i = 1 .. len(arr1)-1: # traiter le reste de arr1
new_dp = [INF] * (p+1)
pour k = 0 .. min(i+1, p):
# 1) garder arr1[i] s'il maintient l'ordre strict
Si arr1[i] > dp[k]:
new_dp[k] = arr1[i]

# 2) remplacer arr1[i] par le plus petit élément arr2 > dp[k-1]
si k > 0 et dp[k-1] != INF:
# recherche binaire en arr2 pour le premier élément strictement supérieur à dp[k-1]
x = élément le plus petit dans arr2 qui est > dp[k-1]
si x existe:
new_dp[k] = min(new_dp[k], x)

dp = new_dp
«» "

Après la boucle, la réponse est la plus petite `k` telle que `dp[k] != INF'.
S'il n'existe pas de «k», retourner «-1».

---

- Oui. 4. Analyse de la complexité

Laissez

* `m = len(arr1)`
* `n = len(arr2)`
* `p = min(m, n)` – la réponse maximale que nous devons considérer

Étape Coût
- Oui.
Tri de `arr2`" `O(n log n)` Autres
"O(m * p * log n)" – pour chacune des positions `m` nous itérerons jusqu'au nombre de swaps `p`, et chaque swap a besoin d'une recherche binaire (`log n`). Autres
Mémoire : 'O(p)' – tableau DP unidimensionnel. Autres

Avec `m` et `n` jusqu`à `5·104`, cela fonctionne confortablement dans les limites.

---

- Oui. 5. Mise en œuvre des références (Python 3)

'`python
bisect d'importation
de taper l'importation Liste

INF = 10**18

Solution de classe:
def make ArrayIncroising(self, arr1: List[int], arr2: List[int]) -> Int:
arr2.sort() # nous avons seulement besoin d'une liste triée
m, n = len(arr1), len(arr2)
p = min(m, n) # limite supérieure sur les swaps nécessaires

# dp[k] = la dernière valeur minimale du préfixe après avoir utilisé exactement k swaps
dp = [INF] * (p + 1)
dp[0] = arr1[0] # aucun échange sur le premier élément

# nous pouvons également utiliser un swap sur le premier élément (toute valeur arr2)
si n > 0:
dp[1] = min(arr1[0], arr2[0])

pour i à portée (1, m):
new_dp = [INF] * (p + 1)
pour k dans la plage (0, min(i + 1, p) + 1):
1. Gardez arr1[i]
Si arr1[i] > dp[k]:
new_dp[k] = arr1[i]

# 2. remplacer arr1[i] si nous avons au moins un échange
si k > 0 et dp[k - 1] != INF:
# trouver le plus petit élément arr2 > dp[k-1]
idx = bisect.bisect_right(arr2, dp[k - 1])
si idx < n:
new_dp[k] = min(new_dp[k], arr2[idx])

dp = new_dp

# réponse est le plus petit k avec une valeur réalisable
pour k dans la plage (p + 1):
si dp[k] != INF:
retour k
retour -1
«» "

---

- Oui. 6. Alternative: mise en œuvre Java (optimisée par l'espace)

"Java
Importation de java.util.*;

solution de classe publique {
public int makeArrayIncreasing(int[] arr1, int[] arr2) {
int m = arr1.longueur, n = arr2.longueur;
int p = Math.min(m, n);
INF longue finale = Long.MAX_VALUE / 4;

Tableau 3.

long[] dp = nouveau long[p + 1];
les tableaux.fill(dp, INF);
dp[0] = arr1[0];
si (n > 0) dp[1] = Math.min(arr1[0], arr2[0];

pour (int i = 1; i < m; i++) {
long[] newDp = nouveau long[p + 1];
Arrays.fill(nouveauDp, INF);
pour (int k = 0; k <= Math.min(i + 1, p); k++) {
// 1. conserver arr1[i]
si (arr1[i] > dp[k]) newDp[k] = arr1[i];

// 2. remplacer arr1[i]
si (k > 0 && dp[k - 1] != INF) {
int idx = upperBound(arr2, dp[k - 1]); // premier > dp[k-1]
si (idx < n) newDp[k] = Math.min(newDp[k], arr2[idx]);
}
}
dp = nouveauDp;
}

pour (int k = 0; k <= p; k++) si (dp[k] != INF) retour k;
retour -1;
}

// Recherche binaire pour le premier élément > cible
Int privé supérieurBound(int[] a, longue cible) {
int l = 0, r = longueur;
pendant que (l < r) {
Int m = (l + r) >>> 1;
si (a[m] <= cible) l = m + 1;
autres r = m;
}
retour l;
}
}
«» "

---

- Oui. 7. Vérification rapide

Scénario : échange minimum ? Autres
- C'est pas vrai.
`arr1 = [1,2,3]` (déjà en augmentation)
"arr1 = [3,1,2]", "arr2 = [4,5]" "2" (wap 3→4, 1→5)
"arr1 = [5,4,3]", "arr2 = [1,2]" "-1" (ne peut pas le faire augmenter)

---

Résumé

* Trier `arr2` une fois.
* Utilisez DP où `dp[k]` stocke la dernière valeur minimale possible après les swaps `k`.
* Transition : conserver l'élément courant s'il conserve l'ordre, ou le remplacer par le plus petit élément `arr2` qui est encore plus grand que la valeur préfixe précédente.
* La réponse est le plus petit `k` pour lequel une solution existe.

L'algorithme fonctionne dans la mémoire `O(m · min(m,n) · log n)` et `O(min(m,n))`, en respectant pleinement les limites du problème.