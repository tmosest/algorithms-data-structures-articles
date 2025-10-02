---
titre: LeetCode 2907. Triplets à rentabilité maximale avec augmentation des prix Je...
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
** Explication de la solution**

Pour chaque triplet des indices `i < j < k` la condition

«» "
prix[j] > prix[i] > prix[k]
«» "

doit tenir.
La somme que nous voulons maximiser est

«» "
bénéfice[i] + bénéfice[j] + bénéfice[k]
«» "

Les tableaux sont au plus `1000` longue – une solution `O(n2)` est déjà rapide
Assez.
L'idée clé est de pré-calculer, pour chaque indice *left* possible `i`,
le meilleur profit possible du partenaire "k" :

«» "
rightBest[i] = max{ profit[k] i et prix[k] < prix[i] }
«» "

Une fois que `rightBest` est connu, nous devons seulement regarder un indice intermédiaire `j` et
essayer tous les indices de gauche possibles `i` qui satisfont `prix[i] < prix[j]`.
Si `rightBest[i]` existe, la valeur candidate est

«» "
profit[i] + bénéfice[j] + droitBest[i]
«» "

et nous gardons le maximum sur tous ces candidats.

-----------------------------------------------------------------------------------

Algorithme
«» "
n ← prix. longueur
droite Meilleur ← tableau de la taille n, toutes les valeurs = ---

// 1) calculer le meilleur partenaire droit pour chaque index de gauche i
pour i = 0 ... n-1
le meilleur ←
pour k = i+1 ... n-1
si prix[k] < prix[i]
meilleur ← max(meilleur , bénéfice[k])
rightBest[i] ← le meilleur

// 2) rechercher le meilleur indice moyen j
réponse ←
pour j = 0 ... n-1
pour i = 0 ... j-1
si prix[i] < prix[j] et droitBest[i] −
candidat ← bénéfice[i] + bénéfice[j] + droitBest[i]
réponse ← max(réponse , candidat)

réponse de retour // (utilisez 64 bits entier)
«» "

-----------------------------------------------------------------------------------

Preuve d'exactitude

Nous prouvons que l'algorithme rend le maximum de profit possible.

---

Lemma 1
Pour chaque indice `i` la valeur `rightBest[i]` calculée à l'étape 1 est égale
"max{ profit[k]) k > i et prix[k] < prix[i] }".
Si un tel `k` n'existe pas, `rightBest[i]` est défini à `---.

**Prof.**

La boucle intérieure de l'étape 1 examine tous les indices `k` avec `k > i`.
Chaque fois que `prix[k] < prix[i]`, `bénéfice[k]` est considéré pour le maximum.
Ainsi, après la finition de la boucle intérieure, `meilleure' équivaut au bénéfice maximal de
tous les indices à droite de "i" dont le prix est inférieur à "prix [i]".
Enfin "droite" Le meilleur est fixé à ce maximum.
Si aucune qualification `k` n'existe, la boucle interne ne met jamais à jour `meilleur`,
Ainsi, il reste à `−. *



Lemma 2
Pour chaque indice intermédiaire `j` et chaque indice gauche `i < j` avec
«prix[i] < prix[j]», si un partenaire de droit valide existe,
`bénéfice[i] + bénéfice[j] + droitBest[i]` est le bénéfice maximal de tous
triplets `(i , j , k)` qui utilisent ce `i` comme index de gauche
et `j` comme indice intermédiaire.

**Prof.**

Corriger `i` et `j`.
Par Lemma 1, `rightBest[i]` est le maximum `bénéfice[k]` parmi tous
indices `k > j` satisfaisant `prix[k] < prix[i]`.
Tout triplet `(i , j , k)` avec la commande de prix requise doit utiliser
exactement un tel "k".
Ainsi le meilleur troisième composant possible est "rightBest[i]",
et le bénéfice total est `bénéfice[i] + bénéfice[j] + droitBest[i]`.



Lemma 3
Au cours de l'étape 2, l'algorithme considère chaque triplet valide
`(i , j , k)` qui satisfait `i < j < k` et `prix[j] > prix[i] > prix[k]`.

**Prof.**

Prends un tel triplet.
Au cours de l'étape 2, la boucle externe choisit `j` comme indice intermédiaire.
La boucle intérieure imite sur tout `i` avec `i < j`.
Depuis `prix[i] < prix[j]`, la condition dans la boucle intérieure est remplie.
Pour cela `i` nous avons aussi un `k` valide avec `prix[k] < prix[i]`;
par Lemma 1 `rightBest[i] -.
Par conséquent, le candidat calculé pour cette paire `(i , j)` est
exactement le bénéfice du triplet original. *



Lemma 4
Pour chaque paire valide `(i , j)` le bénéfice du meilleur triplet qui utilise
`i` comme la gauche et `j` comme le milieu n'est jamais plus petit que la
la valeur candidate examinée par l'algorithme.

**Prof.**

Par Lemma 2 la valeur candidate est le bénéfice maximum réalisable
avec la valeur fixée "(i, j)".
Par conséquent, aucun autre triplet avec les mêmes indices de gauche et de milieu ne peut
produire un profit plus élevé. *



C'est vrai. Théorème
L'algorithme renvoie le bénéfice maximum possible sur tous les triplets
exécuter la commande de prix.

**Prof.**

Que `OPT' soit le profit optimal.

* Existence. *
Par Lemma 3, l'algorithme évalue le bénéfice de chaque triplet valide,
ainsi évalue également le triplet optimal et obtient un candidat
valeur d'au moins "OPT".
"Réponse ≥ OPT".

*Optimalité. *
L'algorithme maintient le maximum de tous les candidats examinés à l'étape 2.
Chaque candidat correspond à un triplet valide (Lemma 4).
Ainsi, la réponse ne peut pas être plus grande que la réponse de l'OPT.
Par conséquent, `réponse = OPT`.



-----------------------------------------------------------------------------------

Analyse de complexité

«» "
Étape 1 : temps O(n2) , mémoire supplémentaire O(n)
Étape 2 : temps O(n2) , O(1) mémoire supplémentaire
«» "

Avec `n ≤ 1000` le programme répond facilement aux limites.

-----------------------------------------------------------------------------------

#### Mise en œuvre de la référence (C++)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
// utiliser 64-bit entier pour le calcul, retourner
long maxProfit(vecteur<int> prix, vecteur<int> bénéfice) {
int n = (int)price.size();
Const longue longue NEG_INF = LLONG_MIN / 4; // sentinelle sûre

/* étape 1: meilleur partenaire droit pour chaque index de gauche */
vector<long long> rightBest(n, NEG_INF);
pour (int i = 0; i < n; ++i) {
long long best = NEG_INF;
pour (int k = i + 1; k < n; ++k) {
si (prix[k] < prix[i]) //
best = max(meilleur, (long)bénéfice[k]);
}
rightBest[i] = meilleur;
}

/* étape 2: essayer chaque indice moyen */
longue réponse = NEG_INF;
pour (int j = 0; j < n; ++j) {
pour (int i = 0; i < j; ++i) {
si (prix[i] < prix[j] && rightBest[i] != NEG_INF) {
long long cand = (long)profit[i] + profit[j] + rightBest[i];
réponse = max(réponse, cand);
}
}
}
réponse de retour; // résultat 64-bit
}
};
«» "

La mise en œuvre suit exactement l'algorithme prouvé correct ci-dessus
et satisfait aux limites de temps/espace requises.