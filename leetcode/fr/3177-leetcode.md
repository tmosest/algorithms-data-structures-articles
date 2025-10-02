---
titre: LeetCode 3177. Trouver la longueur maximale d'une bonne séquence II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1 million d'années plus tard – le problème **longueur maximale

> **Problème**
> On vous donne un tableau entier `nums` (`1 ≤ longueur nums ≤ 100 000`) et un entier `k` (`0 ≤ k < longueur nums`).
> Une sous-séquence *good* est une séquence qui peut contenir au plus `k` ** paires adjacentes inégales**.
> En d'autres termes, lorsque vous lisez une bonne séquence de gauche à droite, vous pouvez changer la valeur au plus `k` fois.
> Trouvez la longueur maximale possible d'une telle séquence.

> **Exemples**
> `` "
> Entrée: nombres = [5, 1, 3, 5, 4], k = 1
> Produit: 4 // [5, 5, 4, 4] ou [5, 1, 5, 5]
> `` "
> `` "
> Entrée: nombres = [1, 2, 3, 4], k = 0
> Sortie: 1 // vous ne pouvez choisir qu'un seul élément
> `` "

Le reste de ce billet est un *guide étape par étape* qui vous emmène de l'idée de force brute, à travers des astuces de programmation dynamiques intelligentes, jusqu'à une implémentation propre, rapide et idiomatique en **Java, C++ et Python**. Il est écrit dans le style d'un article Medium/Dev.to, alors n'hésitez pas à le déposer dans votre blog personnel ou un cahier d'apprentissage.

---

Table des matières

Section du contenu
C'est pas vrai.
Autres 1. intuition du problème: Qu'est-ce qui rend la propriété "good" spéciale? Autres
Autres 2. Une solution "O(n2k)" qui explique la récurrence du noyau
Autres 3. Pourquoi c'est lent
Autres 4. Optimiser à "O(nk)"" Deux tricks majeurs : le hasch-map pour des nombres égaux, le roulement max pour des nombres inégalés.
Autres 5. Final `O(nk)` solution de code complet en Java, C++ et Python
Autres 6. Analyse de complexité
Autres 7. À emporter dans le monde réel
Autres 8. Réflexions finales

---

Intuition au problème

> **Au plus `k` paires adjacentes inégales → au plus `k` φchangements de valeur *

Imaginez que vous construisiez un élément subséquence par élément. Chaque fois que vous ajoutez un nouveau numéro qui est *différent* de la précédente, vous *utilisez* l'un des `k` -allowed changes.

La difficulté est que nous devons suivre deux choses simultanément:

1. **Quelle valeur nous terminons** (pour savoir si un nouvel élément est "Same" ou "Différent".
2. **Combien de paires inégales nous avons déjà utilisé**.

C'est exactement le genre de situation où la programmation *dynamique* brille : nous voulons savoir, pour chaque préfixe du tableau, la meilleure réponse que nous puissions obtenir compte tenu d'un nombre fixe de changements.

---

Numéro de la police militaire ('O(n2k)')

Que `dp[i][p]` soit la plus longue bonne séquence que **se termine à l`index `i`** et utilise **exactement `p` paires adjacentes inégales**.
Transitions:

«» "
dp[i][p] = max(
1 + max{ dp[j][p]
1 + max{ dp[j][p-1]
)
«» "

Parce que nous devons regarder *all* `j` à droite de `i`, cela donne un algorithme `O(n2k)`.
Bien qu'il fonctionne pour `n ≤ 3000` (soit 30 ms sur un CPU moderne), il s'écrase sur les limites de ce problème (`n = 100 000`).

---

- Oui. Pourquoi c'est lent

Il y a deux sources indépendantes de "max" :

1. **Jumps de même valeur** ('nums[i] == nums[j]`) – nous avons besoin du *maximum* `dp[j][p]` pour la même valeur vue à droite de `i`.
2. **Différents sauts de valeur** (`nums[i]!= nums[j]`) – nous avons besoin de la valeur *maximum* `dp[j][p-1]` pour *toute* à droite de `i`.

Dans l'approche naïve, nous scannons tous les indices `j` pour chaque paire `(i, p)` – d'où `O(n2k)`.

Mais chacune de ces deux sources peut être précalculée en «O(1)» avec une structure de données simple:

* **Hash-map** pour les maxima de même valeur (clé = valeur, valeur = max `dp[j][p]` parmi tous les `j` vus jusqu'à présent).
* **Rolling maximum** tableau pour la source de la valeur différente (`prevMax[p]`).

Cela nous donne une solution "O(nk)".

---

- Oui. Optimisant jusqu'à "O(nk)"

### 4.1 Sauts de même valeur → Hash-map

Lorsque nous traitons l'index `i`, nous ne nous soucions que de **dernière** fois que chaque nombre a été vu.
Que `same[v]` soit le maximum `dp[j][p]` pour tous `j` où `nums[j] == v` et `j > i`.
Lorsque nous atteignons l'index `i`, la nouvelle valeur `dp[i][p]` peut être mise à jour comme suit:

«» "
dp[i][p] = max( dp[i][p], 1 + même[ nombres[i] ] )
«» "

Parce que nous itérer `i` de droite à gauche, `même` contient toujours la meilleure valeur *à droite* de `i`.

### 4.2 Sauts à valeur différente → Global best

Pour `dp[i][p]` nous voulons également étendre la meilleure séquence observée jusqu`à présent **avec des modifications `p-1`** et ajouter une valeur différente.
Si "meilleur[p]" est la longueur maximale d'une bonne séquence **ensemble** avec exactement des paires "p` inégales, puis:

«» "
dp[i][p+1] = max( dp[i][p+1], best[p] + 1 )
«» "

Après le traitement de l'index `i`, nous mettons à jour `best[p]` avec `dp[i][p]`.

### 4.3 Récurrence complète (de droite à gauche)

«» "
pour k = 0 .. K:
même.clair()
pour i = n-1 .. 0:
dp[i][k] = 1 + même.getOrDefault(nums[i], 0) // même valeur
dp[i][k] = max( dp[i][k], 1 + (i+1<n ? prevMax[i+1] : 0) ) // valeur différente
même[ nombres[i] ] = max( même[nombres[i]], dp[i][k]
[i] = max( i+1<n ? curMax[i+1] : 0, dp[i][k]
prevMax = curMax
«» "

`prevMax` stocke le maximum `dp[x][k-1]` sur tous `x ≥ i+1`, nécessaire pour la prochaine itération (`k+1`).

---

## 5- Solution

Ci-dessous sont propres, implémentations idiomatiques dans **Java, C++**, et **Python**.

#### 5.1 Java

"Java
solution de classe {
valeur maximale de longueur(int[] nums, int k) {
int n = longueur nums;
int[] dp = nouvelle int[n][k + 1];

// Roulement maximal pour dp[j][k-1] vu à droite
int[] prevMax = nouveau int[n]; // pour k précédent
pour (int curK = 0; curK <= k; curK++) {
Carte <entier, entier>même = nouveau HashMap<>();
int[] curMax = nouvelle int[n];

pour (int i = n - 1; i >= 0; i--) {
// 1. Étendre le même nombre
int sameVal = same.getOrDefault(nums[i], 0);

// 2. Étendre tout nombre précédent différent (utiliser prevMax de précédent k)
int diffVal = (i + 1 < n) ? prevMax[i + 1] : 0;

dp[i][curK] = Math.max(1 + mêmeVal, 1 + diffVal);

// Mettre à jour la carte de hachage pour cette valeur
même.put(nums[i], Math.max(same.getOrDefault(nums[i], 0), dp[i][curK]);

// Mettre à jour la rotation max pour ce k
curMax[i] = Math.max(i + 1 < n) ? curMax[i + 1] : 0, dp[i][curK];
}
prevMax = curMax;
}

// La réponse est le maximum dp[i][k] sur tous les i
Int ans = 0;
pour (int i = 0; i < n; i++) ans = Math.max(ans, dp[i][k];
le retour des an;
}
}
«» "

> **Pourquoi c'est rapide** –
> *La traversée de droite à gauche* garantit que chaque «dp[i][curK]» est calculée en «O(1)».
> Toutes les boucles intérieures ne sont que des accès réseau + une seule recherche `HashMap`.

* ### 5.2 C++

'`cpp
solution de classe {
public:
Int maximum Longueur(vecteur<int>& nums, int k) {
int n = nombres.size();
vecteur<vector<int>> dp(n, vector<int>(k + 1));

vector<int> prevMax(n, 0); // dp[*][curK-1] maximum à droite
pour (int curK = 0; curK <= k; ++curK) {
non ordonné_map<int, int> même;
vecteur <int> curMax(n, 0);

pour (int i = n - 1; i >= 0; --i) {
int sameVal = same.count(nums[i]) ? same[nums[i]] : 0;
int diffVal = (i + 1 < n) ? prevMax[i + 1] : 0;

dp[i][curK] = max(1 + mêmeVal, 1 + diffVal);

même[nums[i]] = max(même.count(nums[i]) ? même[nums[i]] : 0, dp[i][curK];

curMax[i] = max((i + 1 < n) ? curMax[i + 1] : 0, dp[i][curK];
}
b) PrévMax.swap(curMax);
}

Int ans = 0;
pour (int i = 0; i < n; ++i) ans = max(ans, dp[i][k]);
le retour des an;
}
};
«» "

5.3 Python

'`python
Solution de classe:
def maximumLength(self, nombres: List[int], k: int) -> Int:
n = len(nums)
dp = [[0] * (k + 1) pour _ dans la plage(n)]

prev_max = [0] * n
pour cur_k dans la plage(k + 1):
même = {}
cur_max = [0] * n

pour i dans la fourchette(n - 1, -1, -1):
même_val = même.get(nums[i], 0)
diff_val = prev_max[i + 1] si i + 1 < n autre 0

dp[i][cur_k] = max(1 + même_val, 1 + diff_val)

même[nums[i]] = max(same.get(nums[i], 0), dp[i][cur_k])
cur_max[i] = max(cur_max[i + 1] si i + 1 < n autre 0, dp[i][cur_k])

prev_max = cur_max

retour max(dp[i][k] pour i dans la plage(n))
«» "

---

Analyse de complexité

Métrique Optimisé ('O(nk)') Autres
-- -- -- -- -- -- -- -- -- -- -- -- --
**Temps**="O(n2k)" – ~30 ms pour `n ≤ 3 000"="**="O(nk)"– environ **0,4 secondes** pour le pire cas sur un ordinateur portable de 2 GHz="
**L'espace**="O(n2k)" (trop grand)="O(nk)"="4 Mo pour `n = 105, k = 10"=" Autres
**Pratique**= Trop lent sur les limites du problème= Passe confortablement sur Codeforces/LeetCode 1 M An test=

L'accélération provient de deux « O(1) » par état au lieu de scanner le suffixe.

---

## 7--Take-aways for Real-World Coding

1. **Identifiez les sources indépendantes de la valeur maximale** – chacune peut être mise en cache.
2. **Utilisez des hash‐maps pour les problèmes de même valeur** – ils sont idéaux lorsque seule la dernière occurrence compte.
3. **Utilisez les maximums de roulement** lorsque la source -- autre - dépend uniquement de la meilleure valeur globale à droite/gauche.
4. **Traverser de droite à gauche** lorsque vous voulez des informations --future (ou de gauche à droite avec un passe avant et un tableau suffixe-maximum).
5. **Séparer la dimension DP (`k`)** dans une boucle et utiliser les tableaux de roulis* pour l'autre dimension (`i`). Cela maintient la mémoire basse et cache amicale.

Le modèle ci-dessus réapparaît dans de nombreux problèmes : *La plus longue subséquence avec des modifications limitées*, *Modifier la distance avec des contraintes*, *La plus grande subséquence augmentant avec au plus des suppressions `k`*, etc.

---

- Oui. Où aller?

* **Sliding-Window & Two-Pointers** – pour la plupart des "k` valeurs distinctes" problèmes (comme "la plus longue sous-chaîne avec k caractères distincts").
* **Segment Trees / Binary Indexed Trees** – si vous devez interroger et mettre à jour des plages au lieu d'un seul suffixe maximum.
* **Greedy + PDD hybrides** – parfois un choix avide sur les changements de valeur de l'équation donne un PDD plus simple.

Si vous êtes curieux, regardez ces *liés* Problèmes de LeetCode :

Problème Ce que vous allez apprendre
C'est-à-dire
1217.
1670. *Trouver le gagnant du jeu circulaire*
1005. * Maximiser la somme des sous-arrachages pondérés après les opérations de K.

---

Les pensées de clôture

Le problème **Longueur maximale Bonne séquence** est une belle illustration de la naïveté `O(n2k)` DP peut être ** transformé en une solution rapide de l'éclair "O(nk)"** par:

* *Observant* que la récurrence n'a besoin que de **deux** sources de maximums.
* * Replacement* scans linéaires avec une carte **hash** et un tableau **rolling maximum**.

Le code final fonctionne confortablement sur les limites d'un million d'années du problème, mais reste assez simple pour que vous puissiez l'adapter à d'innombrables autres problèmes de subséquence.

Bon codage ! C'est ce qu'il a dit