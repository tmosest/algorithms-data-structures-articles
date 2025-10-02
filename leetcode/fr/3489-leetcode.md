---
titre: LeetCode 3489. Zero Array Transformation IV -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
** Explication de la solution**

Pour chaque requête

«» "
[L , r , v]
«» "

vous pouvez choisir *any* sous-ensemble des indices `l ... r` et diminuer chaque indice choisi par `v`.
Les requêtes doivent être appliquées dans l'ordre donné – nous sommes autorisés à utiliser seulement le premier `k`
requêtes et nous devons décider le plus petit `k` qui peut transformer le tableau entier en
zéros.

-----------------------------------------------------------------------------------

C'est vrai. 1. Observations

*Pour un indice fixe `i`*
seules les requêtes dont la plage contient `i` sont utiles.
Si nous regardons les premières requêtes `k`, le multiset

«» "
D(i , k) = { v de toutes les requêtes 0 ... k-1 qui couvrent i }
«» "

est l'ensemble de nombres que nous sommes autorisés à ajouter (en tant que sous-ensemble) à la valeur actuelle de
'i'.
`i` peut devenir zéro **iff** nous pouvons choisir un sous-ensemble de `D(i , k)` dont la somme est exactement
«nums[i]».

*Monotonicité*
Si un certain `k` fonctionne, chaque `k' ≥ k` plus grand peut seulement ajouter plus de nombres à chaque `D(i,k)`,
d'où il fonctionne aussi.
Donc le prédicat "k` est suffisant"* est monotone – nous pouvons binaire-recherche pour le premier
"k" qui le satisfait.

-----------------------------------------------------------------------------------

C'est vrai. 2. Algorithme de haut niveau

«» "
si tous les nombres sont déjà zéro → réponse = 0

construire D(i,*) pour chaque i une fois (prétraitement)
recherche binaire sur k [1 ... m]
si faisabilité(k) = vrai → élevé = k
Autre faible = k + 1
si aucun k ne fonctionne → réponse = -1
«» "

La partie centrale est le test de faisabilité** pour un «k» donné.

-----------------------------------------------------------------------------------

2.1 Essai de faisabilité – somme de sous-ensemble par indice

Pour chaque indice `i` nous avons le vecteur

«» "
vals[i] = liste de tous (v , requêteIndex) qui couvrent i
«» "

Toutes les paires sont stockées dans l'ordre croissant de `queryIndex`.

Pour un `k` particulier, nous ne conservons que les paires dont `queryIndex < k`:

«» "
candidat = { v de (v,idx) en vals[i] idx < k }
«» "

Maintenant, nous devons décider si un sous-ensemble de «candidat» sommes à «nums[i]».
C'est le problème classique 0/1 knapsack (subset-sum) et peut être résolu avec un
PDD booléen de la taille `cible + 1` (`cible = nombres[i]`).

Parce que le nombre total de valeurs qui peuvent être insérées dans un DP est la longueur de
`candidate`, le temps d'exécution d'une vérification de faisabilité est

«» "
* sur i (=candidate(i)) × nombres[i] )
«» "

«nums[i]» **10 000** (la déclaration garantit que la somme des
les éléments du tableau sont ≤ 10 000), donc un simple tableau DP de cette taille est assez rapide.

-----------------------------------------------------------------------------------

C'est vrai. 3. Preuve d'exactitude

Nous prouvons que l'algorithme renvoie le nombre minimal de requêtes ou `-1`.

---

Lemma 1
Pour un indice fixe `i` et un indice fixe `k`,
`i` peut devenir zéro après avoir appliqué les premières requêtes `k`
**iff** existe un sous-ensemble de `D(i , k)` dont la somme est égale à `nums[i]`.

**Prof.**

*Si partie:*
Supposons qu'un tel sous-ensemble existe.
Appliquer les requêtes correspondantes les unes après les autres – chaque requête qui contient ` Les "
est utilisé exactement une fois sur les indices choisis, en diminuant la valeur de "i" par le
somme du sous-ensemble.
Une fois toutes les requêtes `k` traitées, la valeur de `i` est `nums[i] - somme = 0'.

*Uniquement si partie:*
Si après toutes les requêtes `k` la valeur de `i` est zéro,
chaque fois qu'une requête qui couvre `i` a été appliquée nous avons soit diminué `i` par `v` ou
n'a pas touché du tout.
Ainsi, l ' ensemble de tous les 'v` qui ont été utilisés sur `i` est un sous-ensemble de `D(i, k)` et sa somme est
exactement "nums[i]". *



Lemma 2
Si un certain «k» satisfait à l'essai de faisabilité (c'est-à-dire que tous les indices peuvent être mis à zéro),
alors tout `k' > k` le satisfait aussi.

**Prof.**

Toutes les requêtes avec les indices `k ... k'-1` sont *new* et sont ajoutées à chaque `D(i , k') "
comme éléments supplémentaires.
Par conséquent, chaque sous-ensemble possible pour `k` est toujours possible pour `k'`.
Par conséquent, l'essai de faisabilité est toujours vrai. *



Lemma 3
Pendant la recherche binaire, le prédicat
Les premières requêtes `k` sont suffisantes
est monotone.

**Prof.**

Conséquence directe de Lemma 2.



Lemma 4
Si l ' essai de faisabilité déclare qu ' un certain < < k > > est réalisable,
alors l'algorithme ne produit jamais une valeur inférieure à `k`.

**Prof.**

La recherche binaire rétrécit seulement l'intervalle `[faible, élevé]` tout en maintenant le
propriété que tous les indices à l'intérieur `[faible, élevé]` contenir au moins un "k" réalisable "
(Lemma 3).
Si le test pour `k` est vrai, l'algorithme définit `high = k`; sinon il définit
`faible = k+1`.
Par conséquent, l'espace de recherche est toujours une gamme contiguë de valeurs possibles "k",
et il ne sautera jamais un plus petit possible "k".



Lemma 5
Si l'algorithme produit `-1`, aucun nombre de requêtes ne peut zéror le tableau.

**Prof.**

L'algorithme teste `k = m` (toutes les requêtes).
Si même cela échoue, pour chaque index `i` le multiset `D(i , m)` ne contient pas de
le sous-ensemble résume à "nums[i]".
Ajouter plus de requêtes ne peut pas aider car toutes les requêtes sont déjà présentes.
Ainsi, il est impossible avec un certain nombre de requêtes. *



C'est vrai. Théorème
L'algorithme retourne

* le nombre minimal de requêtes qui peuvent transformer des «nums» en un tableau de tous les zéros,
ou
* `-1` si c'est impossible.

**Prof.**

Si tous les éléments de `nums` sont déjà zéro, l'algorithme retourne `0`,
Ce qui est évidemment minime.

Sinon, nous effectuons une recherche binaire sur `[1 ... m]`.
Par Lemma 3 le prédicat est monotone, donc la recherche binaire convergera vers le
le plus petit "k" possible.
L'essai de faisabilité est correct par Lemma 1.
Si même le maximum `k = m` est impossible, par Lemma 5, la réponse est `-1`.

D'où l'algorithme produit toujours la valeur requise. *



-----------------------------------------------------------------------------------

C'est vrai. 4. Analyse de la complexité

Laissez

* `n` – longueur du tableau (`n` est petit, par exemple ≤ 100),
* `m` – nombre de requêtes (`m` peut être grand, par exemple ≤ 105),
* `S` – la valeur maximale d'un élément dans `nums` (`S` ≤ 10 000, garantie par la
l'énoncé du problème).

«» "
Prétraitement:
Pour chaque requête, nous insérons sa valeur dans chaque index de sa plage.
O(nombre total de paires) ( ≤ n · m dans le pire des cas, mais faible dans la pratique)

Essai de faisabilité pour un k donné:
Pour chaque indice i:
build la liste de tous les v qui viennent des requêtes < k → O(=candidate=)
exécuter sous-ensemble-sum DP de taille nombres[i]+1 en utilisant les valeurs decandidate
→ O(=candidate==1 · nombres[i])
Total pour un essai: O( -----------------

Recherche binaire :
Essais de faisabilité

Durée totale: O( (n·k·S) · log m ) – assez rapide pour les limites
(n ≤ 50, S ≤ 10 000, m ≤ 5 000 dans les essais officiels).

Mémoire :
Pour chaque index, nous stockons au plus des valeurs `k` (une par requête de couverture).
O( n·m ) entiers dans le pire des cas, mais bien au-dessous de 1 Go pour les limites données.
«» "

-----------------------------------------------------------------------------------

C'est vrai. 5. Mise en œuvre des références (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int minZeroArray(vecteur<int>& nombres, vecteur<vecteur<int>>& requêtes) {
n = (int)nums.size();
int m = (int)queries.size();

- Oui. Pré-traitement : valeurs avec leur index de requête --------- */
vecteur<vector<pair<int,int>>> valsByIndex(n); // (v , requêteIndex)
pour (int q = 0; q < m; ++q) {
int l = requêtes[q][0], r = requêtes[q][1], v = requêtes[q][2];
pour (int i = l; i <= r; ++i)
valsByIndex[i].push_back({v, q});
}

/* --------- helper : peut-on faire tous les indices zéro en utilisant les premières requêtes k ? ----- */
auto faisable = [&](int k)->bool {
pour (int i = 0; i < n; ++i) {
// collecte toutes les v des requêtes < k qui couvrent i
vecteur<int> cand;
pour (auto [v, idx] : valsByIndex[i])
si (idx < k) cand.push_back(v);

cible int = nombres[i];
si (cible) 0) continuer; // déjà zéro

// 0/1 knapsack (somme du sous-ensemble)
vecteur <char> dp(cible + 1, 0);
dp[0] = 1;
pour (int x : cand) {
pour (int t = cible; t >= x; --t)
si (dp[t - x]) dp[t] = 1;
}
si (!dp[target]) retourne false; // impossible pour cet index
}
retour true; // tous les indices peuvent être mis à zéro
};

- Oui. Recherche binaire sur k
si (faisable(0)) retourner 0; // tous les nombres déjà zéro

int low = 1, high = m;
réponse int = -1;
alors que (faible <= haut) {
int milieu = faible + (élevé - faible) / 2;
si (facile(milieu)) {
réponse = milieu;
élevé = milieu - 1;
} autre {
faible = milieu + 1;
}
}
réponse de retour; // sera -1 si aucun k ne fonctionne
}
};

/* - Oui. Code de conduite du juge (non requis dans la présentation officielle) --------- */
Int main() {
Solution sol;
vecteur<int> nombres = {12,3};
vecteur<vecteur<int>> requêtes = {{0,2}, {1,2,1}, {0,2}};
cout << sol.minZeroArray(nums, requêtes) << endl; // Sortie: 2
retour 0;
}
«» "

Le programme suit exactement l'algorithme prouvé correct ci-dessus et
conforme au compilateur C++17. Il peut être directement copié dans le LeetCode
éditeur ou tout environnement C++17.