---
titre: LeetCode 3346. Fréquence maximale d'un élément après les opérations I -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
** Explication de la solution**

Pour chaque essai

* «n» – nombre d'amis («1 ≤ n ≤ 2·10^5)
* `k` – distance maximale qu'un ami peut changer (`k` peut être grande)
* `numOps` – nombre d'opérations pouvant être effectuées
* `a[1 ... n]` – distance de l'ami i-e de la station

Au cours d'une opération, nous choisissons un ami et changeons sa distance.
Après toutes les opérations, toutes les distances doivent être un entier.



-----------------------------------------------------------------------------------

C'est vrai. 1. Observation – que signifie faire un groupe?

Tous les amis qui appartiennent à un groupe doivent enfin avoir la même distance.
Pour un groupe qui deviendra la valeur 'x "

«» "
pour chaque ami du groupe :=Distance originale – x= ≤ k
«» "

Toutes les distances à l'intérieur du groupe doivent donc se trouver dans un intervalle de
longueur `2k` (la différence entre le plus petit et le plus grand
la distance originale dans le groupe est au maximum «2k».

Pour une valeur cible fixe `x` nous pouvons choisir *any* sous-ensemble d'amis
dans cet intervalle – nous sommes autorisés à laisser certains amis inchangés
et nous ne changerons que les autres.

-----------------------------------------------------------------------------------

C'est vrai. 2. Deux types de groupes optimaux

*1. La valeur cible est l ' une des distances initiales*
Si la valeur finale est déjà présente dans l'entrée, chaque ami
distance diffère de cette valeur par au plus `k` peut être déplacé vers elle
(1 opération par ami).
La taille d'un tel groupe est égale

«» "
nombre d'amis à l'intérieur [x – k , x + k] (1)
«» "

et nous avons besoin d'une opération pour chaque ami qui n'est pas déjà égal à
"x".

*2. La valeur cible est **non** une distance initiale*
La distance cible peut être n'importe quel entier.
Tous les amis dans un intervalle de longueur `2k` peuvent être déplacés à la même
valeur (1 opération par ami qui diffère de cette valeur).
La taille du groupe est

«» "
nombre d'amis dans un certain intervalle de longueur 2k (2)
«» "

et nous pouvons utiliser au plus `numOps` de ces amis.

La réponse finale est le plus grand des meilleurs groupes de type (1) et
type (2).

-----------------------------------------------------------------------------------

C'est vrai. 3. Comment trouver le meilleur groupe de type (1)

Triez toutes les distances.
Pour chaque distance distincte `v`

«» "
cnt[v] = nombre d'occurrences de v (précalculé)
«» "

Laissez le tableau trié être `b[0 ... n-1]`.

Pour un `v` fixe nous avons besoin du nombre d'éléments à l'intérieur
«[v – k , v + k]».
Avec deux pointeurs (une fenêtre coulissante) nous pouvons obtenir cela en `O(n)`.

«» "
droite – premier index avec b[right] > v + k (exclusif)
gauche – premier indice avec b[gauche] ≥ v – k
total = droite – gauche (taille de la fenêtre)
«» "

Total – cnt[v]» les amis diffèrent de "v" et doivent être changés.
La taille maximale possible d'un groupe qui correspond finalement à "v" est

«» "
cnt[v] + min(numOps , total – cnt[v]) (3)
«» "

-----------------------------------------------------------------------------------

C'est vrai. 4. Comment trouver le meilleur groupe de type (2)

Encore une fois avec une fenêtre coulissante, nous recherchons le plus long intervalle de
longueur "2k".
Maintenant la fenêtre est définie par

«» "
b[à droite] – b[à gauche] ≤ 2k
«» "

La taille de la fenêtre est `droite – gauche + 1`.
La taille maximale de la fenêtre sur toutes les positions est stockée dans
"maxWindow".
Le meilleur groupe de type (2) a une taille

«» "
min(numOps , maxWindow) (4)
«» "

-----------------------------------------------------------------------------------

C'est vrai. 4. Preuve d ' exactitude

Nous prouvons que l'algorithme décrit ci-dessus produit le maximum
nombre possible d'amis qui peuvent enfin avoir la même distance.

---

Lemma 1
Pour une distance fixe `v`, l'algorithme calcule exactement le nombre de
les amis dont la distance initiale se situe dans l'intervalle `[v – k , v + k]`.

**Prof.**

Le tableau est trié.
`right` est avancé alors que `b[right] ≤ v + k`.
Par conséquent, lorsque la boucle s'arrête, `b[right]` est le premier élément plus grand
que `v + k`; tous les éléments précédents appartiennent à l'intervalle.
Pareillement, `gauche` est avancée alors que `b[gauche] < v – k`,
donc `b[gauche]` est le premier élément qui n'est pas inférieur à "v – k".
Tous les indices dans `[gauche , droite-1]` appartiennent à "[v – k , v + k]",
aucun autre indice ne le fait.
Ainsi, la taille de la fenêtre `droite – gauche` est exactement le nombre de
amis dans cet intervalle. *



Lemma 2
Pour une distance fixe `v` la valeur calculée par la formule (3)
est le nombre maximum d'amis qui peuvent être déplacés à distance `v`
utilisant au plus `num Opérations.

**Prof.**

Tous les amis dans l'intervalle `[v – k , v + k]` peut être déplacé vers `v "
(1 opération par ami qui n'est pas déjà à 'v').
Le nombre de ces amis est `total – cnt[v]`.
Nous pouvons utiliser au plus `numOps` d'entre eux, donc la taille du groupe
ne peut dépasser `cnt[v] + min(num Opérations, total – cnt[v]»
qui est exactement la valeur (3).
D'autre part, nous pouvons atteindre cette taille en déplaçant
`min(numOps , total – cnt[v])` amis à `v`.
Par conséquent, la valeur (3) est optimale pour la cible "v".



Lemma 3
`maxWindow` calculé par la deuxième fenêtre coulissante est le maximum
nombre possible d'amis qui peuvent appartenir à un groupe
la distance se trouve à l'intérieur d'un intervalle de longueur "2k".

**Prof.**

Alors que le pointeur droit se déplace de gauche à droite,
le pointeur gauche est toujours le plus petit indice tel que
«b[à droite] – b[à gauche] ≤ 2k».
Par conséquent, la fenêtre `[gauche , droite]` contient toujours tous les éléments
dans un certain intervalle de longueur `2k` et aucune fenêtre plus grande se terminant à
"droit" est possible.
L'algorithme maintient la plus grande taille de fenêtre sur toutes les positions,
d'où `maxWindow` est le nombre maximum d'amis qui peuvent être mis
dans le même groupe en utilisant une distance finale arbitraire. *



Lemma 4
Le nombre optimal d'amis qui peuvent enfin avoir la même distance
est `max( best_type1 , best_type2 )`,
où

«» "
best_type1 = max sur tous les v de (cnt[v] + min(numOps , total(v)-cnt[v]))
best_type2 = min(numOps , maxWindow)
«» "

**Prof.**

*Les groupes de type (1)*: par Lemma 2 le meilleur groupe pour chaque "v" est
exactement la valeur en (3).
Prendre le maximum sur tous les `v` donne `best_type1`.

*Les groupes de type (2)*: par Lemma 3 le plus grand groupe possible à l'intérieur
tout intervalle de longueur `2k` contient `maxWindow` amis.
Seules les "numOps" peuvent être modifiées, donc le maximum réalisable
taille est `min(numOps , maxWindow) = best_type2`.

Tout arrangement final valide doit appartenir à l'un des deux types,
d'où l'optimum global est la plus grande des deux valeurs. *



C'est vrai. Théorème
L'algorithme produit le nombre maximum possible d'amis qui peuvent
être déplacé à la même distance entière en utilisant au plus des opérations "numOps".

**Prof.**

L'algorithme évalue les deux expressions
Lemma 4 et produit leur maximum.
Par Lemma 4 cette valeur est exactement le nombre optimal d'amis
qui peuvent partager la même distance. *



-----------------------------------------------------------------------------------

C'est vrai. 4. Analyse de la complexité

«» "
Tri : O(n log n)
Deux fenêtres coulissantes : O(n)
Consommation de mémoire : O(n)
«» "

Avec `n ≤ 2·10^5 ́ le programme satisfait facilement aux limites.



-----------------------------------------------------------------------------------

C'est vrai. 5. Mise en œuvre des références (Python 3)

'`python
importations
Importations provenant des collections Compteur

def resouver() -> Aucun:
données = sys.stdin.read().strip().split()
si ce n'est pas des données:
retour
it = iter(données)
n = int(next(it))
k = int(next(it))
num_ops = int(next(it))
a = [int(next(it)) pour _ dans la plage(n)]

a.sort()
cnt = contre(a) nombre d'occurrences de chaque valeur

Le meilleur groupe avec une cible égale à une distance initiale
gauche = 0
droite = 0
best1 = 0
pour v dans set(a): # valeurs distinctes
si droite < a.index(v): La droite est toujours devant la gauche
droite = a.index(v)
alors que droite < n et a[droite] <= v + k:
droite += 1
à gauche < n et a[gauche] < v - k:
gauche += 1
total = droite - gauche nombre d'éléments dans [v-k , v+k]
besoin = total - cnt[v] # amis qui ne sont pas déjà à v
possible = cnt[v] + min(num_ops, besoin)
si possible > best1:
best1 = possible

# -------- meilleur groupe avec cible PAS dans les distances initiales ------
gauche = 0
_fenêtre max = 0
pour droite à portée(n):
alors que a[droite] - a[gauche] > 2 * k:
gauche += 1
fenêtre = droite - gauche + 1
si fenêtre > _fenêtre maximale :
max_window = fenêtre
best2 = min(num_ops, max_window)

print(max(best1, best2))

si __nom__ == "__main__" :
résoudre()
«» "

Le programme suit exactement l'algorithme prouvé correct ci-dessus
et est conforme au format d'entrée/sortie requis.