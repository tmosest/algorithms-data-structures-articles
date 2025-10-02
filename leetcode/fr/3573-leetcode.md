---
titre: LeetCode 3573. Meilleur moment pour acheter et vendre Stock V -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
** Explication de la solution**

Pour chaque jour nous connaissons le cours des actions `A[i]`.
Pendant toute la période, au maximum `K` *transactions* peuvent être effectuées.

Une transaction peut être

* **normal** – acheter à jour `i` et vendre à jour `j` (`i < j`);
* ** court** – vendre le jour `i` et racheter le jour `j` (`i < j`).

Après une transaction, l'argent entier est à nouveau en espèces, donc une nouvelle
la transaction ne peut commencer que **après** la précédente a été terminée.
Alors qu'une transaction est toujours en cours, nous sommes soit

«» "
tenant un stock acheté – nous avons payé le prix, nous attendons de vendre
tenant un court vendu – nous avons reçu le prix, nous attendons de racheter
«» "

-----------------------------------------------------------------------------------

C'est vrai. 1. États

Pour chaque niveau de transaction `t ( 0 ... K ) "

«» "
res[t] – meilleur bénéfice total après les transactions t (en espèces)
buy[t] – meilleur bénéfice si nous détenons actuellement un stock acheté dans
la t‐ième transaction (en attente de vente)
vente[t] – meilleur bénéfice si nous détenons actuellement un stock vendu à découvert
dans la t-ième transaction (attente de rachat)
«» "

`acheté` et `vendu` sont définis uniquement pour la transaction *next*
(`acheté[t]` / `vendu[t]` appartiennent au numéro de transaction `t+1`),
Leur taille est `K` (et non `K+1`).

Toutes les valeurs sont conservées en entiers signés 64 bits – un prix peut atteindre
`109`, `K ≤ 100`, le résultat s'intègre facilement dans un entier de 64 bits signé.

-----------------------------------------------------------------------------------

C'est vrai. 2. Transition pour un prix `a = A[i] "

Nous balayons les jours de gauche à droite, traitant le prix `a` une fois.
Pour chaque niveau de transaction `j` (en cours **en arrière** de `K` à `1`) nous
mettre à jour les trois tableaux :

«» "
1) Terminer une transaction maintenant

res[j] peut rester inchangé,
ou nous pouvons terminer une transaction normale:
acheté[j-1] + a
ou terminer une transaction courte:
vendu[j-1] - a

res[j] = max( res[j], acheté[j-1] + a, vendu[j-1] - a )

2) Commencer une nouvelle transaction (normale) à ce jour
nous pouvons ouvrir une position "achetée" pour la transaction j

acheté[j-1] = max( acheté[j-1], res[j-1] - a )

3) Commencer une nouvelle transaction (courte) ce jour
nous pouvons ouvrir une position "vente courte" pour la transaction j

vendu[j-1] = max( vendu[j-1], res[j-1] + a )
«» "

Les boucles sont exécutées en arrière (décroissant) parce que
`acheté[j-1]` et `vendu[j-1]` sur la droite appartiennent encore à la
niveau de transaction précédent «j-1».
Si nous utilisions une boucle vers l'avant, nous écraserions des valeurs qui sont toujours
nécessaire dans la même itération.

-----------------------------------------------------------------------------------

C'est vrai. 3. Preuve d'exactitude

Nous prouvons que l'algorithme rend le maximum de profit possible.

---

Lemma 1
Après traitement des premiers prix `i` (`A[0...i]`),
«res[j]» égal au bénéfice total maximal réalisable après au plus "
opérations effectuées (normales ou courtes) en utilisant seulement ces "i+1".

**Prof.**

Induction sur "i".

*Base `i = 0`*
Avant le premier jour «res[0] = 0» (pas d'argent dépensé, pas de transaction)
terminée).
Pour `j>0` aucune transaction ne peut être terminée, donc
`res[j] = 0` qui est optimal. La lemme tient.

*Étape d'initiation*
Supposons que le lemma tient après le jour `i-1`.
Pendant l'itération pour le jour `i` l'algorithme considère toutes les façons de
*finir une transaction le jour `i` (cas 1).
Toutes les possibilités qui terminent une transaction le jour `i` utilisent l'optimal
le bénéfice de la veille («res[j-1]»), le bénéfice optimal
tenant une position achetée/courte («acheté[j-1]» /
`vendu[j-1]`), puis le nouveau prix `a`.
Ainsi, le maximum sur ces trois possibilités est exactement le meilleur
profit après avoir effectué des transactions `j` les premiers `i+1` jours.
«res[j]» ne peut être amélioré autrement parce que tous les autres Etats
soit garder une transaction déjà terminée (`res[j]` inchangé) ou
effectuer une transaction inachevée (traitée dans les deux autres tableaux). *



Lemma 2
Après traitement des premiers prix "i",
`acheté[j]` égale le bénéfice maximal qui peut être réalisé
après avoir effectué au maximum des opérations "j" ** et**
acheté des actions qui ont été achetées dans la transaction `j+1` le jour `i+1`.

**Prof.**

Induction sur "i".
La mise à jour dans step 2 utilise le profit optimal «res[j-1]» des
niveau de transaction antérieur et soustrait le prix actuel.
Par conséquent, `bought[j]` est exactement le profit optimal pour une normale ouverte
transaction de niveau `j+1`.
Aucun autre changement de mise à jour `bought[j]`, d'où le lemma tient. *



Lemma 3
Après traitement des premiers prix "i",
`vendu[j]` est égal au bénéfice maximal qui peut être réalisé après avoir terminé
au plus des transactions «j» et qui détiennent encore un stock de
transaction `j+1` le jour `i+1`.

**Prof.**

Analogue à Lemma 2, utilisant step 3 de la transition. *



Lemma 4
Pendant la mise à jour pour un prix fixe `a` et le niveau de transaction `j`,
les missions

«» "
res[j] = max(res[j], acheté[j-1] + a, vendu[j-1] - a)
acheté[j-1] = max(acheté[j-1], res[j-1] - a)
vendu[j-1] = max(vendu[j-1], res[j-1] + a)
«» "

maintenir l'invariant de Lemma 1, Lemma 2 et Lemma 3 pour
tous les indices `< j` sont inchangés et mettent à jour correctement les entrées de `j "
et "j-1".

**Prof.**

*Case 1 – Terminer une transaction. *
L'algorithme examine les trois possibilités qui mettent fin à une transaction
à ce jour et garde le maximum; aucune autre stratégie ne peut produire une
un bénéfice plus élevé pour «res[j]».

*Case 2 – début d'une nouvelle transaction normale. *
`bought[j-1]` n'est utilisé que si une transaction est terminée plus tard
jour ou plus tard.
Prendre le maximum de sa valeur actuelle et le bénéfice d'un nouvel achat
(`res[j-1] - a`) donne la valeur optimale pour une position achetée ouverte.

*Case 3 – Commencer une nouvelle transaction courte. *
Même raisonnement pour `vendu[j-1]`.

L'ordre rétrograde de "j" garantit que les valeurs de la droite
côté appartiennent toujours au niveau de transaction précédent, donc les mises à jour
sont corrects. *



Lemma 5
Après traitement de tous les prix, `res[K]` est égal au bénéfice total maximal
réalisable après au plus des transactions "K".

**Prof.**

Par Lemma 1 après le dernier jour (`i = N-1`) le tableau `res` contient
le bénéfice optimal pour chaque transaction compte `0...K`.
Plus de transactions ne peuvent jamais diminuer le bénéfice,
par conséquent, l'entrée pour `K` est le meilleur bénéfice réalisable avec *à
la plupart des transactions "K". *



C'est vrai. Théorème
L'algorithme produit le bénéfice total maximal qui peut être obtenu par
effectuer au maximum des opérations normales ou courtes de type « K » pendant
toujours détenir au plus une unité de stock.

**Prof.**

De Lemma 5 la valeur retournée par l'algorithme est la meilleure
profit. Par conséquent, l'algorithme est correct. *



-----------------------------------------------------------------------------------

C'est vrai. 4. Analyse de la complexité

«» "
Laisser N = , K ≤ 100
«» "

La boucle extérieure exécute des temps `N`, la boucle intérieure exécute des temps `K`.

«» "
Durée : O(N · K) ≤ 5·104 · 100 = 5·106 opérations
Mémoire : O(K) ≤ 100 entiers 64 bits
«» "

Les deux limites sont bien en deçà des contraintes du problème.

-----------------------------------------------------------------------------------

C'est vrai. 5. Mise en œuvre des références (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long long maximumProfit(vecteur<int>& A, int K) {
Int N = (int)A.size();
Si (K) 0) retour 0;

Const longue INF_NEG = -(1LL << 60); // grand nombre négatif

vecteur <long> res(K + 1, 0); // res[0] = 0
vector<long long> acheté(K, INF_NEG); // acheté[t] -> transaction t+1
vectorielle <long long> vendu(K, INF_NEG); // vendu[t] -> transaction t+1

pour (int a : A) { // scan jours de gauche à droite
pour (int j = K; j >= 1; --j) {
// 1) terminer une transaction maintenant
long termeNormal = acheté[j - 1] + a; // acheté[j-1] peut être -INF
longue finale Court = vendu[j - 1] - a; // vendu[j-1] peut être -INF
res[j] = max(res[j], max(finishNormal, finishShort)

// 2) commencer une transaction normale à ce jour
acheté[j - 1] = max(acheté[j - 1], res[j - 1] - a);

// 3) commencer une transaction courte à ce jour
vendu[j - 1] = max(vendu[j - 1], res[j - 1] + a);
}
}
retourner res[K];
}
};
«» "

Le programme suit exactement l'algorithme prouvé correct ci-dessus et
conforme aux limites de temps et de mémoire du problème.