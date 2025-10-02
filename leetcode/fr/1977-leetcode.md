---
titre: LeetCode 1977. Nombre de façons de séparer les nombres -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
** Explication de la solution**

Pour la chaîne `num` nous devons la diviser en un ou plusieurs entiers.
Tous les entiers doivent

* ne contiennent pas de zéros avant
(«012» n'est pas autorisé, «0» seul n'est pas autorisé)
* être **non-diminution** de gauche à droite

Les nombres peuvent être arbitrairement grands – par exemple l'entrée
`"123456789123456789123456789"" contient un entier à 27 chiffres qui
Ne pas entrer dans un entier de 64 bits.

-----------------------------------------------------------------------------------

C'est vrai. 1. Comparaison de deux nombres égaux

Si nous nous scissions, nous devons souvent décider si

«» "
num[i .. i+len-1] <= num[j .. j+len-1] (les deux sous-chaînes ont la même longueur)
«» "

Si nous convertissons chaque sous-chaîne en un `BigInteger` la comparaison
le coût est "O(len)" et toute la programmation dynamique deviendrait
«O(n3)» – beaucoup trop lent pour «n ≤ 500».

Nous ** précalculons un rang pour chaque sous-chaîne d'une longueur fixe**.
Le grade est un entier qui est

«» "
rang[i][len-1] = la position de la sous-chaîne
à partir de i et ayant une longueur len
dans la liste triée de toutes les sous-chaînes de cette longueur
«» "

Si deux sous-chaînes ont la même longueur, alors

«» "
num[i .. i+len-1] <= num[j .. j+len-1]
rang[i][len-1] <= rang[j][len-1]
«» "

Nous pouvons donc comparer des nombres de longueur égale dans `O(1)` heure
après la construction de la table de classement.

-----------------------------------------------------------------------------------

C'est vrai. 2. Bâtir tous grades – tri des seau

Pour une longueur fixe "len" il suffit de regarder le chiffre *len-th*
de toutes les positions de départ possibles.
Parce que les chiffres sont seulement `0 ... 9`, nous pouvons seauter tous les démarrages
positions par ce chiffre – cela prend `O(10)` travail par groupe.

La construction avance longueur par longueur:

«» "
groupes = [ toutes les positions de départ 0 ... n-1 ]

pour len = 1 ... n
nouveaux Groupes = liste vide
pour chaque groupe en groupes
Seau[0 ... 9] = listes vides
pour chaque position p dans le groupe
idx = p + len - 1
si idx < n // la sous-chaîne existe
chiffre = nombre[idx]
Seau[numérique].add(p)
ajouter tous les seaux non vides aux nouveauxGroupes

// attribuer des grades consécutifs
indice de classement = 0
pour le groupe dans les nouveaux groupes
pour la position p dans le groupe
rang[p][len-1] = indice de rang
rangIndex++

groupes = nouveaux groupes
«» "

L'algorithme visite chaque paire `(position, longueur)` une fois,
C'est donc l'heure "O(n2)" et la mémoire "O(n2)".

-----------------------------------------------------------------------------------

C'est vrai. 3. Programmation dynamique

Laissez

«» "
dp[i][len-1] = nombre de fractions valides de
le suffixe num[i ... n-1]
où le premier entier (à partir de i)
a au moins des chiffres len (c'est-à-dire sa longueur ≥ len)
«» "

La réponse dont nous avons enfin besoin est «dp[0][1]» –
le nombre de fractionnements de toute la chaîne avec le premier entier
ayant au moins un chiffre.

**Transition* *

Pour un indice de départ fixe `i` et une longueur minimale fixe `len`

«» "
1) Le premier entier peut être plus long que le len.
Toutes ces possibilités sont comptées en dp[i][len] = dp[i][len+1].

2) Le premier entier peut avoir exactement des chiffres len.
Alors le prochain entier doit avoir la même longueur ou plus,
Mais pour le test de l'égalité, nous comparons la même longueur.

j = i + len // position de l'entier suivant
si j + len <= n // le deuxième entier de la même longueur existe
si rang[i][len-1] <= rang[j][len-1]
dp[i][len] += dp[j][len] // le deuxième entier a la même longueur
Autre
si j + len + 1 <= n
dp[i][len] += dp[j][len+1] // le deuxième entier est plus long
«» "

La récurrence utilise seulement des valeurs déjà calculées
(parce que nous itérer "i" de droite à gauche), donc tout le DP
est "O(n2)".

-----------------------------------------------------------------------------------

C'est vrai. 4. Preuve d ' exactitude

Nous prouvons que l'algorithme renvoie le nombre requis de fractionnements.

---

Lemma 1
Pour toutes les positions de départ `a , b` et longueur `len` qui existent tous les deux,
`num[a .. a+len-1] <= num[b .. b+len-1] "
iff `rank[a][len-1] <=rank[b][len-1]`.

**Prof.**

Au cours de la construction du rang pour cette `len` fixe toutes les sous-chaînes
de cette longueur sont séparés en seaux par le premier chiffre
('0 ... 9').
Après cela, les groupes sont remplacés par les seaux, donc le relatif
ordre à l'intérieur d'un seau égale l'ordre des sous-chaînes
avec ce premier chiffre.
Ce processus est répété pour le deuxième chiffre, troisième chiffre, ...
Par conséquent, après toute la boucle pour les finitions "len",
la concaténation de tous les seaux finals est la liste de tous
sous-chaînes de cette longueur triées par ordre numérique ascendant.
Par conséquent, les nombres consécutifs que nous attribuons comme grades sont exactement
les positions triées. *



Lemma 2
`dp[i][len]` correspond au nombre de fractionnements valides du suffixe
«num[i ... n-1]» où le premier entier a au moins des chiffres "len".

**Prof.**

Nous prouvons par induction inverse sur `i` (à partir de `n-1`).

*Base*
Si le suffixe n'a qu'une seule position (`i = n-1`),
le seul fractionnement possible est le chiffre unique "num[i]".
La boucle définit `dp[i][len] = 1` pour le maximum `len` (`len = 1`)
et pour tous les petits "len" utilise la récurrence:
«dp[i][len] = dp[i][len+1] = 1».
C'est ainsi que tient le lemma.

*Étape d'initiation. *
Supposons que le lemma détient pour tous les indices `> i`.
Pour une "len" fixe, la récurrence PD considère

1. **D'abord entier plus long que "len".**
Toutes ces fractionnements sont comptés en «dp[i][len+1]» par le
hypothèse d'induction.

2. **D'abord entier exactement les chiffres `len`. **
L'entier suivant doit être de longueur au moins "len".
* Si l'entier suivant a exactement des chiffres "len`,
il doit être **pas plus petit** que le premier entier.
Par Lemma 1, cela équivaut à
«Rank[i][len-1] <=rank[j][len-1]» où `j = i+len`.
Si cela tient, toutes les scissions du suffixe restant commencent
à `j` avec la première longueur entière `len` sont ajoutés:
«dp[j][len]».
* Sinon le deuxième entier est plus long,
qui est compté par «dp[j][len+1]» (encore par induction).

Toutes les possibilités sont disjointes et couvrent toutes les fractionnements valides de la
suffixe.
Par conséquent, «dp[i][len]» compte exactement le nombre de fractionnements requis.
*



C'est vrai. Théorème
L'algorithme produit le nombre de façons de diviser toute la chaîne
dans des entiers non décroissants sans tête zéro.

**Prof.**

La réponse que nous obtenons est `dp[0][1]` –
fractionnements de la chaîne entière (`i = 0`) où le premier entier
a au moins un chiffre.
Par Lemma 2 c'est précisément le nombre de fractionnements valides.
Toutes les opérations sont effectuées modulo `1 000 000 007`,
donc la valeur retournée est le reste nécessaire. *



-----------------------------------------------------------------------------------

C'est vrai. 4. Analyse de la complexité

«» "
construire tous les rangs : temps O(n2), mémoire O(n2)
programmation dynamique : temps O(n2), mémoire O(n2)
«» "

Pour `n ≤ 500` cela est bien en dessous des limites.



-----------------------------------------------------------------------------------

C'est vrai. 5. Mise en œuvre des références (Kotlin 1.6)

'''kotlin
Importer java.io. BufferedReader
Importer java.io. InputStreamReader
Importer java.util. Tableau
importation java.util.StringTokenizer

val const privée MOD = 1_000_000_007L

fun main() {
val num = readLine()!!.trim()
valeur n = longueur num.
val chiffres = IntArray(n) { num[it] - '0' }

Tableau de classement ---------------------------------- */
// rang[i][len-1] – position de sous-chaîne i.i+len-1
val rang = Array(n) { IntArray(n - it) } // n-i entrées par ligne

// seau pour toutes les longueurs
groupes var: Liste <ArrayList<Int>> = liste mutableOf()
groupes = ArrayList(0 jusqu'à n).toList() // toutes les positions de départ

pour (len in 1..n) {
val newGroupes = liste mutable de <ArrayList<Int>>()
pour (groupe en groupe) {
val seaux = Array(10) { ArrayList<Int>() }
pour (p dans le groupe) {
val idx = p + len - 1
si (idx < n) {
valeur d = chiffres[idx]
les seaux[d].add(p)
}
}
pour (b dans les seaux) si (b.isNotEmpty()) newGroupes.add(b)
}
var rangIndex = 0
pour (grp dans les nouveaux groupes) {
pour (p en grp) rang[p][len - 1] = rangIndex
rangIndex++
}
groupes = nouveaux groupes
}

- Oui. programmation dynamique ------------------------- */
// dp[i][len-1] – nombre de fractions de suffixe i..n-1
// avec un premier entier ayant au moins des chiffres len
val dp = Array(n) { LongArray(n - it) }

pour (i en n - 1 Aux 0) {
si (chiffres [i]] 0) continuer // nombres ne peuvent pas commencer par 0
val maxLen = n - i
pour (lenIdx en maxLen - 1 jusqu'à 0) {
val len = lenIdx + 1
Si (LenIdx < maxLen - 1) {
var ways = dp[i][lenIdx + 1] // premier entier plus long
j = i + len
si (j + len <= n) { // deuxième entier même longueur existe
si [rank[i][lenIdx] <= rank[j][lenIdx] {
Voies += dp[j][lenIdx]
} autre {
si (j + len + 1 <= n) {
Voies += dp[j][lenIdx + 1]
}
}
}
dp[i][lenIdx] = voies % MOD
} autre { // dernière longueur possible
dp[i][lenIdx] = 1L
}
}
}

val reponse = dp[0][0] % MOD
printn(réponse à Int())
}
«» "

Le programme suit exactement l'algorithme prouvé correct ci-dessus
et est entièrement compatible avec Kotlin 1.6.